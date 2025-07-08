# ✅MySQL的优化器的索引成本是怎么算出来的？

# 典型回答


[✅为什么MySQL会选错索引，如何解决？](https://www.yuque.com/hollis666/dr9x5m/ghy5i20ie717exee)



在上面的文章中，我们介绍过，MySQL 是基于成本来选择索引的，并且也列举了一些可能会影响成本的因素，那么具体到细节上，这个成本是如何计算出来的呢？包括哪些内容呢？



其实在 MySQL中，一条 SQL 的成本主要就是包含了 CPU 的成本和 IO的成本两部分

**<font style="color:rgb(59, 67, 81);"></font>**

```java
Cost  =  CPU Cost + IO Cost
```



CPU Cost 表示计算的开销，通过`select * from mysql.server_cost`查看（MySQL 8.0）



![1722058701794-68ab32d7-298b-4429-a011-5eef8f4febc5.png](./img/kdc77sgESalSpZuc/1722058701794-68ab32d7-298b-4429-a011-5eef8f4febc5-567615.png)



主要包含了：



+ disk_temptable_create_cost：创建磁盘临时表的成本
+ disk_temptable_row_cost：磁盘临时表中每条记录的成本
+ key_compare_cost：索引键值比较的成本
+ memory_temptable_create_cost：创建内存临时表的成本
+ memory_temptable_row_cost：内存临时表中每条记录的成本
+ row_evaluate_cost：记录间的比较成本



可以看到，创建临时表的成本是最高的，索引键值比较的成本比较低。



IO Cost 表示引擎层 IO 的开销，通过`select * from mysql.engine_cost`查看（MySQL 8.0）



![1722058927761-0f71cdea-e353-404b-8317-09ed2f4f912f.png](./img/kdc77sgESalSpZuc/1722058927761-0f71cdea-e353-404b-8317-09ed2f4f912f-688555.png)



主要包含了：



+ io_block_read_cost：从磁盘读取一个页的成本
+ memory_block_read_cost：从内存读取一个页的成本



可以看到，从磁盘中读取一个页的成本（1）是从内存中读取一个页的成本（0.25）的4倍。



当我们想看一个 SQL 的执行成本时，可以通过 `explain <font style="color:rgb(77, 77, 76);background-color:rgb(247, 247, 247);"> FORMAT=json </font>`的方式来查看，得到的结果如下：



```java
{
  "query_block": {
    "select_id": 1,
    "cost_info": {
      "query_cost": "4.55"
    },
    "table": {
      "table_name": "collection_inventory_stream",
      "access_type": "ALL",
      "rows_examined_per_scan": 43,
      "rows_produced_per_join": 43,
      "filtered": "100.00",
      "cost_info": {
        "read_cost": "0.25",
        "eval_cost": "4.30",
        "prefix_cost": "4.55",
        "data_read_per_join": "68K"
      },
      "used_columns": [
        "id",
        "gmt_create",
        "gmt_modified",
        "collection_id",
        "changed_quantity",
        "price",
        "quantity",
        "state",
        "saleable_inventory",
        "occupied_inventory",
        "stream_type",
        "identifier",
        "deleted",
        "lock_version"
      ]
    }
  }
}
```



主要关注 cost_info 即可，

+ read_cost 表示就是从Engine读取数据的 IO 成本；
+ eval_cost 表示 Server 层的 CPU 成本；
+ prefix_cost 表示这条 SQL 的总成本；
+ data_read_per_join 表示总的读取记录的字节数。

  
通过这几个指标，我们就能大致分析出，一个 SQL在执行过程中，哪部分成本最高，然后再具体去分析他进一步的原因。比如发现是 IO 成本高，那么就继续分析可能是因为发生了大量的回表，导致磁盘读取的次数比较多，导致了 IO 成本高，进而导致了 SQL 变慢！



> 更新: 2024-07-27 13:49:30  
> 原文: <https://www.yuque.com/hollis666/dr9x5m/waruyhds7gcn6srf>