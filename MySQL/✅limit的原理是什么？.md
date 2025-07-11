# ✅limit的原理是什么？

# 典型回答


在 MySQL 中，`LIMIT` 关键字用于限制查询结果返回的行数。它的原理主要是通过控制查询结果集的返回范围来提高查询效率。`LIMIT` 可以与 `OFFSET` 一起使用，指定从哪一行开始返回数据，并限制返回的最大行数。  



```sql
SELECT * FROM users LIMIT 10; -- 返回 users 表的前 10 行数据
SELECT * FROM users LIMIT 10, 20; -- 第 11 行开始，返回 20 行数据。
```



[✅一个查询语句的执行顺序是怎么样的？](https://www.yuque.com/hollis666/dr9x5m/ihsu18bwvr9csnzu)



### limit执行顺序


在上面的文档中，我们介绍了一个SQL查询语句的执行顺序，可以看到，**limit其实是在最后执行的**，也就是说，在做完筛选、分组、排序等操作之后，最后进行的limit。因为它是对最终结果集的限制。所以在执行完其他所有操作后，才应用 `LIMIT`，从而确保查询返回的结果集已经是经过完整处理的。  



还有就是，limit的查询中，如果是像 `LIMIT 10000, 100` 这种形式 ，他会先查询出全部数据（10000+100），然后丢弃前面的结果，再返回需要的部分。  这也是为什么深分页很慢的原因：



[✅limit 0,100和limit 10000000,100一样吗？](https://www.yuque.com/hollis666/dr9x5m/gtpc5u4i7xmy13el)





### limit执行过程
对于 SQL 查询中 `LIMIT` 的使用，像 `LIMIT 10000, 100` 这种形式，MySQL 的执行顺序大致如下：



1. **从数据表中读取所有符合条件的数据**（包括排序和过滤）。
2. **将数据按照 **`**ORDER BY**`** 排序**。
3. **根据 **`**LIMIT**`** 参数选择返回的记录**：
    - **跳过**前 10000 行数据（这个过程是通过丢弃数据来实现的）。
    - 然后**返回接下来的 100 行数据**。



所以，`LIMIT` 是先检索所有符合条件的数据，然后丢弃掉前面的行，再返回指定的行数。这解释了为什么如果数据集很大，`LIMIT` 会带来性能上的一些问题，尤其是在有很大的偏移量（比如 `LIMIT 10000, 100`）时。





### 为什么不跳过前面数据
为什么不是直接跳过前面的数据，而是要全部查到之后再丢弃呢？主要是为了确保结果集按照 `ORDER BY` 进行正确排序。例如你要跳过前 10000 行，但是没排序的情况下你不知道前10000行是哪些数据，是没办法跳过的。





### limit的优化


以上是limit的基本原理，实际上这个过程还是比较慢的，性能也是比较差的，所以limit还有一些单独的优化：

[https://dev.mysql.com/doc/refman/8.4/en/limit-optimization.html](https://dev.mysql.com/doc/refman/8.4/en/limit-optimization.html) 



以下是我做的翻译，和一些解释：



1、针对没有HAVING的limit语句，如果你只使用使用 `LIMIT`查询少量行，MySQL 会在优先考虑使用索引，而不是像通常那样进行全表扫描。 因为索引天然有序，这样就能在扫描时直接按照索引顺序进行，减少读取和排序的开销  



2、 如果将 `LIMIT row_count` 与 `ORDER BY` 结合使用，MySQL 在找到排序结果中的前 `row_count` 行之后就停止排序，而不是对整个结果集进行排序。如果排序是通过使用索引完成的，会非常快。如果必须进行文件排序（`filesort`），则会先选择所有匹配查询条件且没有 `LIMIT` 子句的行，然后对它们进行排序，直到找到前 `row_count` 行为止。找到初始行之后，MySQL 不会再对剩余的结果集进行排序。  



<font style="background-color:#FBDE28;">注意，很多人看到这里会觉得和上面的说法矛盾了，我第一次看的时候也有这个疑惑，到底是全部排序后抛弃，还是排序够了就停止呢？其实这里说的是两种情况：</font>

<font style="background-color:#FBDE28;"></font>

+ `LIMIT row_count`如果和`ORDER BY`结合使使用，则在找到前row_count就停止。
+ `LIMIT offset,row_count`如果和`ORDER BY`结合使使用，则对整个结果集完成排序后，再抛弃前offset行。



3、 如果将 `LIMIT row_count` 与 `DISTINCT` 结合使用，MySQL 会在找到 `row_count` 个唯一的行后停止。  



4、 `LIMIT 0` 会快速返回一个空的结果集。这对于检查查询的有效性非常有用。



5、 如果 `ORDER BY` 不使用索引，但查询中有 `LIMIT` 子句，优化器可能会避免使用合并文件，而是使用内存中的文件排序操作来对行进行排序。  



> 更新: 2025-03-15 15:54:23  
> 原文: <https://www.yuque.com/hollis666/dr9x5m/zfvodtm4bk19eyvb>