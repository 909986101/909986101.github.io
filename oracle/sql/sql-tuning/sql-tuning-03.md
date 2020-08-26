# 执行计划

SQL 执行缓慢有很多原因。

如果是数据库自身原因导致 SQL 缓慢，需要通过分析等待事件，做出相应处理。

单纯的 SQL 优化，更侧重于分析 SQL 写法，分析 SQL 的执行计划。

SQL 调优就是通过各种手段和方法使优化器选择最佳执行计划，以最小的资源消耗获取到想要的数据。

## 获取执行计划常用方法

### 使用 AUTOTRACE 查看执行计划

利用 SQLPLUS 中自带的 AUTOTRACE 工具查看执行计划。

```
SQL> set autot
Usage: SET AUTOT[RACE] {OFF | ON | TRACE[ONLY]} [EXP[LAIN]] [STAT[ISTICS]]
```

|命令|描述|
|:-|:-|
|`set autot on`|运行 SQL 并且显示运行结果、执行计划和统计信息|
|`set autot trace`|运行 SQL，但不显示运行结果，显示执行计划和统计信息|
|`set autot trace exp`|不执行查询语句，DML 语句会执行。只显示执行进化|
|`set autot trace stat`|运行 SQL，只显示统计信息|
|`set autot off`|关闭 AUTOTRANCE|

示例

```sql
SQL> conn scott/tiger
显示已连接
SQL> set lines 200 pages 200
SQL> set autot on
SQL> select count(*) from emp;
---返回结果
---（略）
---执行结果
---（略）
---统计信息
---（略）
```

使用 `set autot on` 查看执行计划会输出 SQL 运行结果，如果 SQL 返回大量结果，可以使用 `set autot trace`。

利用 AUTOTRACE 查看执行计划会带来一个额外但好处，当 SQL 执行完毕后，会在执行计划但末尾显示 SQL 在运行过程中耗费的一些统计信息。

- `recursive calls` 表示递归调用的次数。一个 SQL 在第一次执行时会发生硬解析，此时优化器会隐含的调用一些内部 SQL。因此当一个 SQL 第一次执行，`recursive calls` 会大于 0；再次执行时不需要递归调用，`recursive calls` 会等于 0。

  如果 SQL 语句中含有自定义函数，`recursive calls` 总是大于 0。自定义函数被调用多少次，`recursive calls` 就会显示为多少次。

- `db block gets` 表示有多少个块发生变化。查询语句中 `db block gets` 一般为 0，因为一般情况下，只有 DML 语句才会导致块发生变化。

  不为 0 的情况，有延迟块清除，或者 SQL 语句中调用了返回 CLOB 的函数。

- `consistent gets` 表示逻辑读，单位是块。逻辑读并不是衡量 SQL 执行快慢读唯一标准，需要结合 I/O 等其他综合因素共同判断。进行 SQL 优化时，应设法减少逻辑读个数。

  **如果 SQL 的逻辑读远远大于 SQL 语句中所有表的段大小之和（假设所有表都走全表扫描，表关联方式为 HASH JOIN），那么该 SQL 就存在较大优化空间。**

- `physical reads` 表示从磁盘读取了多少个数据块，如果表已经被缓存在 `buffer cache` 中，没有物理读，`physical reads` 等于 0。

- `redo size` 表示产生了多少字节的重做日志。一般 DML 语句才会产生 redo，查询语句不会产生 redo，所以 redo size 为 0。如果有延迟块清除，查询语句也会产生 redo。

- `bytes sent via SQL*Net to client` 表示从数据库服务器发送了多少字节到客户端。

- `bytes received via SQL*Net from client` 表示从客户端发送了多少字节到服务端。

- `SQL*Net roundtrips to/from client` 表示客户端与数据库服务端交互次数。可以通过设置 arraysize 减少交互次数。

- `sorts(memory)` 和 `sorts(disk)` 分别表示内存排序和磁盘排序的次数。

- `rows processed` 表示 SQL 一共返回多少行数据。

  **做 SQL 优化应最关注这部分数据，根据 SQL 返回到行数判断整个 SQL 应该是走 HASH 连接（`rows processed` 很大）还是嵌套循环（`rows processed` 很小）。**

### 使用 EXPLAIN PLAN FOR 查看执行计划