# 第一章 SQL 优化必懂概念

## 基数（CARDINALITY）

某个列唯一键（Distinct_Keys）的数量叫做基数。比如性别列，该列列值只有男女，所以这一列基数是 2。主键列的基数等于表的总行数。基数的高低影响列的数据分布。

列的唯一键在列中的数据分布不一定平均。如果某个列基数很低，该列数据分布就会非常不均衡，会导致 SQL 查询可能走索引，也可能走全表扫描。

查看列的数据分布

`SELECT 列, count(*) FROM 表 GROUP BY 列 ORDER BY 2 DESC;`

如果 SQL 语句是单表访问，以 5% 为界，返回表中 5% 以内的数据走索引，超过 5% 的时候走全表扫描。

换个说法，具体的唯一键键值在列中的数据分布，导致了走索引还是全表扫描。

## 选择性（SELECTIVITY）

基数与总行数的比值的百分数就是某个列的选择性。

在进行 SQL 优化时，单独看列的基数是没有意义的，基数必须对比总行数才有实际意义，因此引入了选择性这个概念。

当一个列选择性大于 20%，说明该列的数据分布就比较均衡了。

当一个列出现在 WHERE 条件中，该列没有创建索引并且选择性大于 20%，那么该列就必须创建索引，从而提升 SQL 查询性能。如果表只有几百条数据，那我们就不用创建索引了。

### SQL 优化核心思想观点：只有大表才会产生性能问题

干扰项，也许有人会说：“我有个表很小，只有几百条，但是该表经常进行 DML，会产生热点块，也会出性能问题。”这属于应用程序设计问题，不属于 SQL 

### 抓出必须创建索引的列

首先，该列必须出现在 WHERE 条件中。怎么抓取这样的列，有两种方法，一种是通过 `V$SQL_PLAN` 抓取，另一种是通过下面的脚本抓取。

1. 先执行下面的存储过程，刷新数据库监控信息
   
   ```sql
   begin
     dbmd_stats.flush_database_monitoring_info;
   end;
   ```

1. 查询出哪个表的哪个列出现在 WHERE 条件中
   
   ```sql
   SELECT r.name owner,
        o.name table_name,
        c.name column_name,
        equality_preds, --等值过滤
        equijoin_preds, --等值 JOIN 比如 WHERE a.id=b.id
        nonequijoin_preds, --不等 JOIN
        range_preds, --范围过滤次数 > >= < <= between and
        like_preds, --LIKE 过滤
        null_preds, --NULL 过滤
        timestamp
   FROM sys.col_usage$ u, sys.obj$ o, sys.col$ c, sys.user$ r
   WHERE o.obj# = u.obj#
        AND c.obj# = u.obj#
        AND c.col# = u.intcol#
        AND r.name = 'SCOTT'
        AND o.name = 'TEST';
   ```

1. 查询出选择性大于等于 20% 的列
   
   ```sql
   SELECT a.owner,
        a.table.name,
        a.column_name,
        round(a.num_distinct / b.num_rows * 100, 2) selectivity
   FROM dba_tab_col_statistics a, dba_tables b
   WHERE a.owner = b.owner
        AND a.table_name = b.table_name
        AND a.owner = 'SCOTT'
        AND a.table_name = 'TEST'
        AND a.num_distinct / b.num_rows >= 0.2;
   ```

1. 确保这些列没有创建索引
   
   ```sql
   SELECT table_owner, table_name, column_name, index_name
   FROM dba_ind_columns
   WHERE table_owner = 'SCOTT'
        AND table_name = 'TEST'
   ```

把上面的脚本结合起来，我们就可以得到全自动的优化脚本

```sql
SELECT owner,
    column_name,
    num_rows,
    Cardinality,
    selectivity,
    'Need index' as notice
FROM (SELECT b.owner,
        a.column_name,
        b.num_rows,
        a.num_distinct Cardinality,
        round(a.num_distinct / b.num_rows * 100, 2) selectivity
      FROM dba_tab_col_statistics a, dba_tables b
      WHERE a.owner = b.owner
        AND a.table_name = b.table_name
        AND a.owner = 'SCOTT'
        AND a.table_name = 'TEST')
WHERE selectivity >= 20
    AND column_name not in (SELECT column_name
                            FROM dba_ind_columns
                            WHERE table_owner = 'SCOTT'
                                AND table_name = 'TEST')
    AND column_name in
        (SELECT c.name
         FROM sys.col_usage$ u, sys.obj$ o, sys.col$ c, sys.user$ r
         WHERE o.obj# = u.obj#
            AND c.obj# = u.obj#
            AND c.col# = u.intcol#
            AND r.name = 'SCOTT'
            AND o.name = 'TEST');
```

## 直方图（HISTOGRAM）

如果没有对基数低的列收集直方图统计信息，基于成本的优化器（CBO）会认为该列数据分布是均衡的。执行计划里面的 Rows 是假的。执行计划中的 Rows 是根据统计信息以及一些数学公式计算出来的。

在做 SQL 优化的时候，经常需要做的工作就是帮助 CBO 计算出比较准确的 Rows。我们说的是比较准确的 Rows。CBO 永远不可能计算得到精确的 Rows。

如果 CBO 每次都能计算得到精确的 Rows，那么相信我们这个时候只需要关心业务逻辑、表设计、SQL 写法以及如何建立索引了，再也不用担心 SQL 会走错执行计划了。

现在我们对 owner 列收集直方图

```sql
BEGIN
     DBMS_STATS.GATHER_TABLE_STATS(ownname             =>   'SCOTT',
                                   tabname             =>   'TEST',
                                   estimate_percent    =>   100,
                                   method_opt          =>   'for columns owner size skewonly',
                                   no_invalidate       =>   FALSE,
                                   degree              =>   1,
                                   cascade             =>   TRUE);
END;
```

查看一下 owner 列的直方图信息

```sql
SELECT a.column_name,
     b.num_rows,
     a.num_distinct Cardinality,
     round(a.num_distinct / b.num_rows * 100, 2) selectivity,
     a.histogram,
     a.num_buckets
FROM dba_tab_col_statistics a, dba_tables b
WHERE a.owner = b.owner
     AND a.table_name = b.table_name
     AND a.owner = 'SCOTT'
     AND a.table_name = 'TEST'
```

如果 SQL 使用了绑定变量，绑定变量的列收集了直方图，那么该 SQL 就会引起绑定变量窥探。Oracle 11g 引入了自适应游标共享（Adaptive Cursor Sharing）,基本上解决了绑定变量窥探问题，但是自适应游标共享也会引起一些新问题。

当我们遇到一个 SQL 有绑定变量怎么办？其实很简单，我们只需要运行一下语句。

`SELECT 列, count(*) FROM test GROUP BY 列 ORDER BY 2 DESC;`

读者只需要知道直方图是用来帮助 CBO 在对基数很低、数据分布不均衡的列进行 Rows 估算的时候，可以得到更精确的 Rows 就够了。

当列出现在 WHERE 条件中，列的选择性小于 1% 并且该列没有收集过直方图，这样的列就应该收集直方图。

### 抓出必须创建直方图的列

全书第二个全自动化优化脚本

```sql
SELECT a.owner,
     a.table_name,
     a.column_name,
     b.num_rows,
     a.num_distinct,
     trunc(num_distinct / num_rows * 100, 2) selectivity,
     'Need Gather Histogram' notice
FROM dba_tab_col_statistics a, dba_tables b
WHERE a.owner = 'SCOTT'
     AND a.table_name = 'TEST'
     AND a.owner = b.owner
     AND a.table_name = b.table_name
     AND num_distinct / num_rows < 0.01
     AND (a.owner, a.table_name, a.column_name) IN
          (SELECT r.name owner, o.name table_name, c.name column_name
           FROM sys.col_usage$ u, sys.obj$ o, sys.col$ c, sys.user$ r
           WHERE o.obj# = u.obj#
               AND c.obj# = u.obj#
               AND c.col# = u.intcol#
               AND r.name = 'SCOTT'
               AND o.name = 'TEST')
     AND a.histogram = 'NONE';
```

## 回表（TABLE ACCESS BY INDEX ROWID）

当对一个列创建索引之后，索引会包含该列的键值以及键值对应行所在的 rowid。

通过索引中记录的 rowid 访问表中的数据就叫回表。回表一般是单块读，回表次数太多会严重影响 SQL 性能，如果回表次数太多，就不应该走索引扫描了，应该直接走全表扫描。

在进行 SQL 优化的时候，一定要注意回表次数！特别是要注意回表的物理 I/O 次数。

为了消除 arraysize 参数对逻辑读的影响，设置 arraysize=5000。arraysize 表示 Oracle 服务器每次传输多少行数据到客户端，默认为 15。设置了 arraysize=5000 之后，就不会发生一个块被读多次的问题了。

```sql
SET ARRAYSIZE 5000
SET AUTOT TRACE


SELECT owner FROM test WHERE owner='SYS'

SELECT * FROM test WHERE owner='SYS'
```

返回表中 5% 以内的数据走索引，超过表中 5% 的数据走全表扫描。根本原因在于回表。

在无法避免回表的情况下，走索引如果返回数据量太多，必然会导致回表次数太多，从而导致性能严重下降。

Oracle 12c 的新功能批量回表（TABLE ACCESS BY INDEX ROWID BATCHED）在一定程度上改善了单行回表的性能。

`SELECT * FROM table WHERE ...`，这样的 SQL 必须回表，所以我们必须严禁使用 `SELECT *`。

`SELECT COUNT(*) FROM table`，这样的 SQL 就不需要回表。当要查询的列也包含在索引中，这个时候就不需要回表了，所以我们往往会建立组合索引来消除回表，从而提升查询性能。

当一个 SQL 有多个过滤条件但是只在一个列或者部分列建立了索引，这个时候会发生回表再过滤（TABLE ACCESS BY INDEX ROWID 前面有“*”），也需要创建组合索引，进而消除回表再过滤，从而提升查询性能。

## 集群因子（CLUSTERING FACTOR）

集群因子用于判断索引回表需要消耗的物理 I/O 次数。

```sql
--我们先对测试表 test 的 object_id 列创建一个索引 idx_id
CREATE INDEX IDX_ID ON TEST(OBJECT_ID);


--然后我们查看该索引的集群因子
SELECT OWNER, INDEX_NAME, CLUSTERING_FACTOR
FROM DBA_INDEXES
WHERE OWNER = 'SCOTT'
     AND INDEX_NAME = 'IDX_ID'
--集群因子
OWNER      INDEX_NAME CLUSTERING_FACTOR
---------- ---------- -----------------
SCOTT      IDX_ID                  1094


--索引 IDX_ID 的叶子块中有序的存储了索引的键值以及键值对应行所在的 ROWID
SELECT * FROM(SELECT OBJECT_ID, ROWID
               FROM TEST
               WHERE OBJECT_ID IS NOT NULL
               ORDER BY OBJECT_ID)
WHERE ROWNUM <= 5
```

集群因子的算法，根据索引列的有序列值进行计算，相邻的列值所对应的 ROWID 是否在同一个数据块。如果在同一个数据块，集群因子不变；如果不在同一个数据块，那么集群因子加一。

根据算法我们知道**“集群因子介于表的块数和表行数之间”**。
- **如果集群因子与块数接近，说明表的数据基本上是有序的，而且其顺序基本与索引顺序一样。这样在进行索引范围或者索引全扫描的时候，回表只需要读取少量的数据块就能完成。**
- **如果集群因子与表记录数接近，说明表的数据和索引顺序差异很大，在进行索引范围扫描或者索引全扫描的时候，回表会读取更多的数据块。**

集群因子只会影响索引范围扫描（INDEX RANGE SCAN）以及索引全扫描（INDEX FULL SCAN），因为只有这两种索引扫描方式会有大量数据回表。

集群因子不会影响索引唯一扫描（INDEX UNIQUE SCAN），因为索引唯一扫描只返回一条数据。集群因子更不会影响索引快速全扫描（INDEX FAST FULL SCAN），因为索引快速全扫描不回表。

**集群因子影响的是索引回表的物理 I/O 次数。**

重建索引不能降低集群因子，因为表中的数据顺序始终没变。唯一能降低集群因子的办法就是根据索引列排序对表进行重建，但是在实际操作中是不可取的，因为我们无法照顾到每一个索引。

**当索引范围扫描或者索引全扫描不回表，或者返回数据量很少的时候，不管集群因子多大，对 SQL 查询性能几乎没有任何影响。**

当我们把表中所有的数据块缓存在 buffer cache 中，这个时候不管集群因子多大，对 SQL 查询性能也没有多大影响，因为这时不需要物理 I/O，数据块全在内存中访问速度是非常快的。

## 表与表之间关系

表与表之间存在 3 中关系。一对一、一对多和多对多关系。搞懂表与表之间关系，对于 SQL 优化、SQL 等价改写、表设计优化以及分表分库都有巨大帮助。

两表在进行关联的时候，如果两表属于一对一关系，关联之后返回的结果也是属于“一”的关系，数据不会重复。如果两表属于一对多关系，关联之后返回的结果集属于“多”的关系。如果两表属于多对多关系，关联之后返回的结果集会产生局部范围的笛卡尔积，多对多关系一般不存在内/外连接中，只能存在于半连接或者反连接中。

如果不知道业务，不知道数据字典，怎么判断两表是说明关系

```sql
SELECT * FROM EMP E, DEPT D WHERE E.DEPTNO = D.DEPTNO;


--只需要对两表关联列进行汇总统计就能知道两表是说明关系
SELECT DEPTNO, COUNT(*) FROM EMP GROUP BY DEPTNO ORDER BY 2 DESC;

    DEPTNO   COUNT(*)
---------- ----------
        30          6
        20          5
        10          3

SELECT DEPTNO, COUNT(*) FROM DEPT GROUP BY DEPTNO ORDER BY 2 DESC;

    DEPTNO   COUNT(*)
---------- ----------
        10          1
        40          1
        30          1
        20          1
```

从上面查询可以知道两表 emp 和 dept 是多对一关系。

案例

`SELECT COUNT(*) FROM A LEFT JOIN B ON A.ID=B.ID;`

a 与 b 是一对一关系。因为 a 与 b 是使用外连接进行关联，不管 a 与 b 是否关联上，始终都会返回 a 的数据。SQL 语句中求得是两表关联后的总行数，因为两表是一对一关系，关联之后数据不会翻番，那么该 SQL 等价于如下文本。

`SELECT COUNT(*) FROM A;`

如果 a 与 b 是多对一关系，也可以将 b 表去掉，因为两表关联之后数据不会翻番。如果 a 与 b 是一对多关系，就不能去掉 b 表，因为关联之后数据量会翻番。