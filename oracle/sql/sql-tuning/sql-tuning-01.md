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