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
