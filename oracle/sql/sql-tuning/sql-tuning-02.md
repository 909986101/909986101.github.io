# 统计信息

## 什么是统计信息

收集统计信息是为了让优化器选择最佳执行计划，以最小的代价（成本）查询出表中的数据。

统计信息主要分为表、列、索引、系统、数据字典以及动态性能视图基表的统计信息。

表的统计信息主要包括表的总行数（num_rows）、表的块数（blocks）以及行平均长度（avg_row_len），可以通过查询数据字典 `DBA_TABLES` 获取表的统计信息。

```sql
--现在创建一个测试表 T_STATS
CREATE TABLE T_STATS AS SELECT * FROM DBA_OBJECTS;


--查看表 T_STATS 常用的表的统计信息
SELECT OWNER, TABLE_NAME, NUM_ROWS, BLOCKS, AVG_ROW_LEN
FROM DBA_TABLES
WHERE OWNER = 'SCOTT'
    AND TABLE_NAME = 'T_STATS';
--因为 T_STATS 是新创建的表，没有收集过统计信息，所以从 T_STATS 查询数据是空的
OWNER           TABLE_NAME        NUM_ROWS     BLOCKS AVG_ROW_LEN
--------------- --------------- ---------- ---------- -----------
SCOTT           T_STATS


--现在收集表 T_STATS 的统计信息
BEGIN
    DBMS_STATS.GATHER_TABLE_STATS(OWNNAME           => 'SCOTT',
                                TABNAME             => 'T_STATS',
                                ESTIMATE_PERCENT    => 100,
                                METHOD_OPT          => 'for all columns size auto',
                                NO_INVALIDATE       => FALSE,
                                DEGREE              => 1,
                                CASCADE             => TRUE);
END;
/


--再次查看表的统计信息
OWNER           TABLE_NAME        NUM_ROWS     BLOCKS AVG_ROW_LEN
--------------- --------------- ---------- ---------- -----------
SCOTT           T_STATS              72674       1061          97
```

列的统计信息主要包括列的基数、列中的空值数量以及列的数据分布情况（直方图）。可以通过数据字典 `DBA_TAB_COL_STATISTICS` 查看列的统计信息

```sql
--查看表 T_STATS 常用的列统计信息
SELECT COLUMN_NAME, NUM_DISTINCT, NUM_NULLS, NUM_BUCKETS, HISTOGRAM
FROM DBA_TAB_COL_STATISTICS
WHERE OWNER = 'SCOTT'
    AND TABLE_NAME = 'T_STATS'
```

上面的查询中，一至五列分别表示，列名、列的基数、列中 NULL 值的数量、直方图的桶数和直方图类型

在工作中，可以使用下面脚本查看表和列的统计信息

```sql
SELECT A.COLUMN_NAME,
    B.NUM_ROWS,
    A.NUM_NULLS,
    A.NUM_DISTINCT CARDINALITY,
    ROUND(A.NUM_DISTINCT / B.NUM_ROWS * 100, 2) SELECTIVITY,
    A.HISTOGRAM,
    A.NUM_BUCKETS
FROM DBA_TAB_COL_STATISTICS A, DBA_TABLES B
WHERE A.OWNER = B.OWNER
    AND A.TABLE_NAME = B.TABLE_NAME
    AND A.OWNER = 'SCOTT'
    AND A.TABLE_NAME = 'T_STATS';
```

索引的统计信息主要包括索引 blebel（索引高度 -1）、叶子块的个数（leaf_blocks）以及集群因子（clustering_factor）。可以通过数据字典 `DBA_INDEXES` 查看索引的统计信息。

```sql
--在 OBJECT_ID 列上创建一个索引
CREATE INDEX IDX_T_STATS_ID ON T_STATS(OBJECT_ID);


--创建索引的时候会自动收集索引的统计信息，运行下面脚本查看索引的统计信息
SELECT BLEVEL, LEAF_BLOCKS, CLUSTERING_FACTOR, STATUS
FROM DBA_INDEXES
WHERE OWNER = 'SCOTT'
    AND INDEX_NAME = 'IDX_T_STATS_ID';
```
```
    BLEVEL LEAF_BLOCKS CLUSTERING_FACTOR STATUS
---------- ----------- ----------------- ---------------
         1         161              1127 VALID
```

```sql
--如果要单独对索引收集统计信息，可以使用下面脚本收集
BEGIN
    DBMS_STATS.GATHER_INDEX_STATS(OWNNAME   => 'SCOTT',
                                INDNAME     => 'IDX_T_STATS_ID');
END;
/
```

## 统计信息重要参数设置

通常使用下面脚本收集表和索引的统计信息

```sql
BEGIN
    DBMS_STATS.GATHER_TABLE_STATS(OWNNAME           => 'TAB_OWNER',
                                  TABNAME           => 'TAB_NAME',
                                  ESTIMATE_PERCENT  => 根据表大小设置,
                                  METHOD_OPT        => 'FOR ALL COLUMNS SIZE REPEAT',
                                  NO_INVALIDATE     => FALSE,
                                  DEGREE            => 根据表大小，CPU 资源和负载设置,
                                  GRANULARITY       => 'AUTO',
                                  CASCADE           => TRUE);
END;
```

参数
- ownname：表示表的拥有者，不区分大小写。
- tabname：表示表名字，不区分大小写。
- granularity：表示收集统计信息的粒度，该选项只对分区表生效，默认为 AUTO，表示让 Oracle 根据表达分区类型自己判断如何收集分区表的统计信息。对于改选项，一般采用 AUTO 方式，也就是数据库默认方式，因此，在后面的脚本中，省略该选项。
- estimate_percent：表示采样率，范围是 0.000001～100。  
  一般对小于 1GB 的表进行 100% 采样，因为表很小，即使 100% 采样速度也比较块。有时候小表有可能数据分布不均衡，可能会导致统计信息不准。因此建议对小表 100% 采样。  
  一般对表大小在 1GB～5GB 的表采样 50%，对大于 5GB 的表采样 30%。如果表特别大，有几十甚至上百 GB，建议应该先对表进行分区，然后分别对每个分区收集统计信息。  
  一般情况下，为了确保统计信息比较准确，建议采样率不要低于 30%。

  ```sql
  --查看表对采样率
  SELECT OWNER,
         TABLE_NAME,
         NUM_ROWS,
         SAMPLE_SIZE,
         ROUND(SAMPLE_SIZE / NUM_ROWS * 100) ESTIMATE_PERCENT
  FROM DBA_TAB_STATISTICS
  WHERE OWNER='SCOTT' AND TABLE_NAME='T_STATS';
  ```
- method_opt：用于控制收集直方图策略。  
  `method_opt => 'for all columns size 1'` 表示所有列都不收集直方图  
  `method_opt => 'for all columns size skewonly'` 表示对表中所有列收集自动判断是否收集直方图。在实际工作中千万不要使用该方式收集直方图信息，因为并不是表中所有都列都会出现在 where 条件中，对没有出现在 where 条件中的列收集直方图没有意义。  
  `method_opt => 'for all columns size auto'` 表示对出现在 where 条件中的列自动判断是否收集直方图。这是默认值。  
  `method_opt => 'for all columns size repeat'` 表示当前有哪些列收集列直方图，现在就对哪些列收集直方图。  
  `method_opt => 'for columns object_type size skewonly'` 表示单独对 OBJECT_TYPE 列收集直方图，对于其余列，如果之前收集过直方图，现在也收集直方图。

  在实际工作中，需要对列收集直方图就收集直方图，需要删除某列直方图就删除其直方图，当系统趋于稳定之后，使用 REPEAT 方式收集直方图。
- no_invalidate：表示共享池中涉及到该表的游标是否立即失效，默认值为 `DBMS_STATS.AUTO_INVALIDATE`，表示让 Oracle 自己决定是否立即失效。建议将 no_invalidate 参数设置为 FALSE，立即失效。因为有时候 SQL 执行缓慢是因为统计信息过期导致，重新收集统计信息之后执行计划还是没有改变，原因就在于没有将这个参数设置为 FALSE。
- degree：表示收集统计信息的并行度，默认为 NULL。如果表没有设置 degree，收集统计信息的时候就不开并行；如果表设置了 degree，收集统计信息的时候就按照表的 degree 来开并行。可以查询 `DBA_TABLES.degree` 来查看表的 degree，一般情况下，表的 degree 都为 1。建议可以根据当时系统的负载、系统中 CPU 的个数以及表大小来综合判断设置并行度。
- cascade：表示在收集表的统计信息的时候，是否级联收集索引的统计信息，默认值为 `DBMS_STATS.AUTO_CASCADE`，表示让 Oracle 自己判断是否级联收集索引的统计信息。一般将其设置为 TRUE，在收集表的统计信息的时候，级联收集索引的统计信息。

## 检查统计信息是否过期

收集完表的统计信息之后，如果表中有大量数据发生变化，这时表的统计信息就过期来，需要重新收集表的统计信息。如果不重新收集，可能会导致执行计划走偏。

可以使用下面方法检查表统计信息是否过期，先刷新数据库监控信息。

```sql
BEGIN
    DBMS_STATS.FLUSH_DATABASE_MONITORING_INFO;
END;
/
```

```sql
SELECT OWNER, TABLE_NAME, OBJECT_TYPE, STALE_STATS, LAST_ANALYZED
FROM DBA_TAB_STATISTICS
WHERE OWNER_NAME = 'SCOTT'
    AND TABLE_NAME = 'T_STATS';

OWNER      TABLE_NAME      OBJECT_TYPE     STALE_STATS     LAST_ANALYZED
---------- --------------- --------------- --------------- -------------
SCOTT      T_STATS         TABLE           YES             24-MAY-17
```

STALE_STATS 显示为 YES 表示表的统计信息过期来。如果 STALE_STATS 显示为 NO，表示表的统计信息没有过期。

通过下面的查询找出统计信息过期的原因。

```sql
SELECT TABLE_OWNER, TABLE_NAME, INSERTS, UPDATES, DELETES, TIMESTAMP
FROM ALL_TAB_MODIFICATIONS
WHERE TABLE_OWNER = 'SCOTT'
    AND TABLE_NAME = 'T_STATS';

TABLE_OWNER     TABLE_NAME         INSERTS    UPDATES    DELETES TIMESTAMP
--------------- --------------- ---------- ---------- ---------- ---------
SCOTT           T_STATS                  0       9709          0 24-MAY-17
```

从查询结果可以看到，从上一次收集统计信息到现在，表被更新来 9700 行数据，所以统计信息过期来。

Oracle 是怎么判断一个表的统计信息过期来呢？当表中超过 10% 的数据发生变化（INSERT、UPDATE、DELETE），就会引起统计信息过期。

数据字典 ALL_TAB_MODIFICATIONS 还可以用来判断哪些表需要定期降低高水位，比如一个表经常进行 insert、delete，那么这个表应该定期降低高水位，这个表的索引也应该定期重建。除此之外，ALL_TAB_MODIFICATIONS 还可以用来判断系统中哪些表是业务核心表、表的数据每天增长量等。

如果一个 SQL 有多个表关联或者有视图套视图等，怎么快速检查 SQL 语句中所有的表统计信息是否过期呢？

```sql
-- 有如下 SQL
SELECT * FROM EMP E, DEPT D WHERE E.DEPTNO=D.DEPTNO;


-- 可以先用 explain plan for 命令，在 plan_table 中生产 SQL 的执行计划
EXPLAIN PLAN FOR SELECT * FROM EMP E, DEPT D WHERE E.DEPTNO=D.DEPTNO;


-- 然后使用下面脚本检查 SQL 语句中所有的表的统计信息是否过期
SELECT OWNER, TABLE_NAME, OBJECT_TYPE, STALE_STATS, LAST_ANALYZED
FROM DBA_TAB_STATISTICS
WHERE (OWNER, TABLE_NAME) IN (SELECT OBJECT_OWNER, OBJECT_NAME
                              FROM PLAN_TABLE
                              WHERE OBJECT_TYPE LIKE '%TABLE%'
                              UNION
                              SELECT TABLE_OWNER, TABLE_NAME
                              FROM DBA_INDEXES
                              WHERE (OWNER, INDEX_NAME) IN (SELECT OBJECT_OWNER, OBJECT_NAME
                                                            FROM PLAN_TABLE
                                                            WHERE OBJECT_TYPE LIKE '%INDEX%'));

OWNER      TABLE_NAME OBJECT_TYP STALE_STATS     LAST_ANALYZED
---------- ---------- ---------- --------------- -------------
SCOTT      DEPT       TABLE      NO              05-DEC-16
SCOTT      EMP        TABLE      YES             22-OCT-16


-- 最后使用下面脚本检查 SQL 语句统计信息的过期原因
SELECT *
FROM ALL_TAB_MODIFICATIONS
WHERE (TABLE_OWNER, TABLE_NAME) IN (SELECT OBJECT_OWNER, OBJECT_NAME
                                    FROM OBJECT_TYPE
                                    WHERE OBJECT_TYPE LIKE '%TABLE%'
                                    UNION
                                    SELECT TABLE_OWNER, TABLE_NAME
                                    FROM DBA_INDEXES
                                    WHERE (OWNER, INDEX_NAME) IN (SELECT OBJECT_OWNER, OBJECT_NAME
                                                                  FROM PLAN_TABLE
                                                                  WHERE OBJECT_TYPE LIKE '%INDEX%'));
```

## 扩展统计信息

当 WHERE 条件中有多个谓语过滤条件，但是这些谓语过滤条件彼此是有关系的而不是相互独立的，这时可能需要收集扩展统计信息以便优化器能够估算出较为准确的行数（Rows）。

```sql
-- 创建一个表 T
CREATE TABLE T AS
SELECT LEVEL AS ID, LEVEL || 'a' AS a, LEVEL || LEVEL || 'b' AS b
FROM DUAL
CONNECT BY LEVEL < 100;

-- 在 T 表中，知道 A 列的值就知道 B 列的值，A 和 B 这样的列就叫做相关列。


-- 一直执行 INSERT INTO T SELECT * FROM T; 直到 T 表中有 3244032 行数据。


-- 对 T 表收集统计信息
-- 使用 DBMS_STATS.GATHER_TABLE_STATS 进行收集，其中 method_opt 的参数使用 'for all columns size skewonly'
-- 代码略


-- 查看 T 表的统计信息
-- 代码略


-- 创建两个索引
CREATE INDEX IDX1 ON T(a);
CREATE INDEX IDX2 ON T(a, b);


-- 使用如下 SQL 及其执行计划
SELECT * FROM T WHERE a='1a' AND b='11b';
32768 rows selected.

Execution Plan
------------------------------------------------------------------
Plan hash values: 2303463401
-----------------------------------------------------------------------------------
| Id  | Operation                   | Name |  Rows | Bytes | Cost (%CPU)| Time     |
-----------------------------------------------------------------------------------
|   0 | SELECT STATEMENT            |      |   331 |  4303 |    84   (0)| 00:00:02 | 
|   1 |  TABLE ACCESS BY INDEX ROWID| T    |   331 |  4303 |    84   (0)| 00:00:02 |
|*  2 |   INDEX RANGE SCAN          | IDX2 |   331 |       |     3   (0)| 00:00:01 |
-----------------------------------------------------------------------------------

Predicate Information (identified by operation id):
---------------------------------------------------

   2 - access("A"='1a' AND "B"='11b')

Statistics
---------------------------------------------------------------------------
部分略
  ... ...
  ... ...
     32768  rows precessed

-- 优化器估算返回 331 行数据，但是实际上返回了 32768 行数据。
-- 因为优化器不知道 A 与 B 的关系，所以在估算返回行数的时候采用的是：
-- 总行数 * A 的选择性 * B 的选择。
SELECT ROUND(1/99/99*3244032) FROM DUAL;

round(1/99/99*3211032)
----------------------
                   331

-- 因为 A 列的值可以决定 B 列的值，所以上述 SQL 可以去掉 B 列的过滤条件
SELECT * FROM T WHERE a='1a';

32768 rows selected.

-- 这时优化器能正确的估算返回的 Rows。


-- 如果不改写 SQL，而且还能让优化器得到比较准确的 Rows。
--在 Oracle 11g 之前可以使用动态采样（至少 Level 4）。
ALTER SESSION SET OPTIMIZER_DYNAMIC_SAMPLING=4;
-- 执行 SQL 并返回其执行化
-- 代码略
-- 使用动态采样 Level 4 采样之后，优化器估算返回 33845 行数据，实际返回了 32768 行数据，这已经比较精确了。
-- 在 Oracle 11g 以后，可以使用扩展统计信息将相关的列结合成一个列。
SELECT DBMS_STATS.CREATE_EXTENDED_STATS(USER, 'T', '(A, B') FROM DUAL;

DBMS_STATS.CREATE_EXTENDED_STATS(USER, 'T', '(A, B')
--------------------------------------------------------------------------------
SYS_STUNA$6DVXJXTP05EH56DTIR0X

-- 对表重新收集统计信息
-- method_opt 的参数使用 'for columns SYS_STUNA$6DVXJXTP05EH56DTIR0X size skewonly'

-- 查看 T 表的统计信息
-- 代码略
-- 重新收集统计信息之后，扩展列 SYS_STUNA$6DVXJXTP05EH56DTIR0X 也收集了直方图。

-- 再次执行 SQL
-- 代码略
-- 优化器就能够估算出较为准确的 Rows。
```

需要注意的是，扩展统计信息只能用于等值查询，不能用于非等值查询。

## 动态采样

如果一个表从来没有收集过统计信息，默认情况下 Oracle 会对表进行动态采样（Level=2）以便优化器估算出较为准确的 Rows，**动态采样的最终目的就是为了让优化器能够评估出较为准确的 Rows**。

```sql
-- 创建一个测试表
CREATE TABLE T_DYNA AS SELECT * FROM DBA_OBJECT;


-- 执行下面 SQL 并且查看执行计划
SELECT COUNT(*) FROM T_DYNA;

Execution Plan
------------------------------------------------------------
    ... ...
    ... ...
------------------------------------------------------------

Note
-----
   - dynamic sampling used for the statement (level=2)
```

因为表 T_DYNA 是才创建的新表，没有收集过统计信息，所以会启动动态采样。执行计划中 `dynamic sampling used for the statement (level=2)` 表示启用了动态采样，level 表示采样级别，默认情况下采样级别为 2。

动态采用的级别分为 11 级
- level 0：不启用动态采样。
- level 1：当表（非分区表）没有收集过统计信息并且这个表要与另外的表进行关联（不能是单表访问），同时该表没有索引，表的数据块必须大于 32 个，满足这些条件的时候，Oracle 会随机扫描表中 32 个数据块，然后评估返回的 Rows。
- level 2：对没有收集过统计信息的表启用动态采样，采样的块数为 64 个。如果表的块数小于 64 个，则采样全部的块。
- level 3：对没有收集过统计信息的表启用动态采样，采样的块数为 64 个。如果表已经收集过统计信息，但是优化器不能准确的估算出返回的 Rows，而是靠猜，比如 `WHERE SUBSTR(OWNER, 1, 3)`，这时会随机扫描 64 个数据块进行采样。
- level 4：对没有收集过统计信息的表启用动态采样，采样的块数为 64 个。如果表已经收集过统计信息，但是表有两个（及）以上过滤条件（AND/OR），这时会随机扫描 64 个数据块进行采样，相关列问题就必须启用至少 level 4 进行动态采样。level 4 采样包含了 level 3 的采样数据。
- level 5：收集满足 level 4 采样条件的数据，采样的块数为 128 个。
- level 6：收集满足 level 4 采样条件的数据，采样的块数为 256 个。
- level 7：收集满足 level 4 采样条件的数据，采样的块数为 512 个。
- level 8：收集满足 level 4 采样条件的数据，采样的块数为 1024 个。
- level 9：收集满足 level 4 采样条件的数据，采样的块数为 4096 个。
- level 10：收集满足 level 4 采样条件的数据，采样表中所有的数据块。
- level 11：Oracle 自动判断如何采样，采样的块数由 Oracle 自动判定。

启动动态采样

```sql
-- 将动态采样 level 设置为 3
ALTER SESSION SET OPTIMIZER_DYNAMIC_SAMPLING=3
```

添加 HINT 启用动态采样

```sql
SELECT /*+ DYNAMIC_SAMPLING(3) */ * FROM T_DYNA WHERE SUBSTR(OWNER, 4, 3)='LIC';
```

如果表已经收集过统计信息并且优化器能够准确的估算出返回的 Rows，即使添加了动态采样的 HINT 或者是设置了动态采样的参数为 level 3，也不会启用动态采样。

当系统中有全局临时表，就需要使用动态采样，因为全局临时表无法收集统计信息，建议对全局临时表至少启用 level 4 进行采样。

**当执行计划中表的 Rows 估算有严重偏差的时候，例如相关列问题，或者两表关联有多个连接列，关联之后 Rows 算少，或者是 WHERE 过滤条件中对列使用了 SUBSTR、INSTR、LIKE，又或者是 WHERE 过滤条件中有非等值过滤，或者 GROUP BY 之后导致 Rows 估算错误，此时可以考虑使用动态采样，同样，建议动态采样至少设置为 level 4。**

在数据仓库系统中，有些报表 SQL 的过滤条件太复杂，有大量的 AND 和 OR 过滤条件，同时也可能有大量的 WHERE 子查询过滤条件，从而导致优化器不能估算出较为准确的 Rows 而产生了错误的执行计划。可以考虑启用动态采样 level 6 观察性能是否改善。

不要在系统级更改动态采样级别，默认为 2 就行。如果某个表需要启用动态采样，直接在 SQL 语句中添加 HINT 即可。

## 定制统计信息收集策略

要确保统计信息的准确性。优化器在计算执行计划的成本时依赖于统计信息，没有收集统计信息，或者统计信息过期，那么优化器就会出现严重偏差，从而导致性能问题。

数据库自带有 JOB 每天晚上定时收集数据库中所有表的统计信息，如果数据库特别大，自带的 JOB 无法完成全库统计信息收集。可以关闭数据库自带的统计信息收集 JOB，根据实际情况自己定制收集统计信息策略。

```sql
-- 脚本用于收集 SCOTT 账户下统计信息过期或者从未收集过统计信息的表的统计信息，
-- 采样率也根据表的段大小做出了相应调整
DECLARE
    CURSOR STALE_TABLE IS
        SELECT OWNER,
               SEAMENT_NAME,
               CASE
                 WHEN SEGMENT_SIZE < 1 THEN
                    100
                 WHEN SEGMENT_SIZE >= 1 AND SEGMENT_SIZE <= 5 THEN
                    50
                 WHEN SEGMENT_SIZE > 5 THEN
                    30
               END AS PERCENT,
               6 AS DEGREE
        FROM (SELECT OWNER,
                     SEGMENT_NAME,
                     SUM(BYTES / 1024 / 1024 / 1024) SEGMENT_SIZE
              FROM DBA_SEGMENTS
              WHERE OWNER = 'SCOTT' -- SCOTT 账户
                    AND SEGMENT_NAME IN (SELECT TABLE_NAME
                                         FROM DBA_TAB_STATISTICS
                                         WHERE (LAST_ANALYZED IS NULL OR STALE_STATS = 'YES')
                                               AND OWNER = 'SCOTT') -- SCOTT 账户
                                         GROUP BY OWNER, SEGMENT_NAME);
BEGIN
    DBMS_STATS.FLUSH_DATABASE_MONITORING_INFO;
    FOR STALE IN STALE_TABLE LOOP
        DBMS_STATS.GATHER_TABLE_STATS(OWNNAME          => STALE.OWNER,
                                      TABNAME          => STALE.SEGMENT_NAME,
                                      ESTIMATE_PERCENT => STALE.PERCENT,
                                      METHOD_OPT       => 'for all columns size repeat',
                                      degree           => STALE.DEGREE,
                                      CASCADE          => TRUE);
    END LOOP;
END;
/
```

全局临时表无法收集统计信息，可以抓出系统中的全局临时表，抓出系统中使用到全局临时表的 SQL，然后根据实际情况，对全局临时表进行动态采样，或者是人工对全局临时表设置统计信息（DBMS_STATS.SET_TABLE_STATS）。

```sql
-- 脚本抓出系统中使用到全局临时表的 SQL
SELECT B.OBJECT_OWNER, B.OBJECT_NAME, A.TEMPORART, SQL_TEXT
FROM DBA_TABLES A, V$SQL_PLAN B, V$SQL C
WHERE A.OWNER = B.OBJECT_OWNER
      AND A.TEMPORARY = 'Y'
      AND A.TABLE_NAME = B.OBJECT_NAME
      AND B.SQL_ID = C.SQL_ID;
```