# ✅ShardingJDBC 在查询的时候如果没有分表键，他怎么样？

# 典型回答


ShardingJDBC中有一个负责路由的路由引擎，对于带有分片键的SQL，根据分片键的不同可以划分为单片路由(分片键的操作符是等号)、多片路由(分片键的操作符是IN)和范围路由(分片键的操作符是BETWEEN)。 **不携带分片键的SQL则采用广播路由。**



根据SQL类型，**广播路由又可以划分为全库表路由、全库路由、全实例路由、单播路由和阻断路由这5种类型。**

****

![1716628862663-ea6c457d-ea08-4445-96b2-2275b0ac36ff.png](./img/Ez3ZAwrt2hHrOp-W/1716628862663-ea6c457d-ea08-4445-96b2-2275b0ac36ff-515551.png)



一般来说，我们用的是比较多的其实就是 DML操作了，**DML 操作的时候，主要做的就是全库表路由。**



也就是说，当查询语句没有使用分片键时，ShardingJDBC 会将查询语句广播到所有的分片中执行。这意味着每个分片都会独立执行一次查询，然后 ShardingJDBC 会将各个分片的结果汇总并返回给应用。



举个例子，我们的逻辑表t_order，对应的物理表是t_order_01，t_order_02，t_order_03，t_order_00，而你的 SQL 是：

```plain
SELECT * FROM t_order WHERE user_name = "Hollis";
```



那么他其实在执行时，执行的是以下 SQL：



```plain
SELECT * FROM t_order_00 WHERE user_name = "Hollis"
UNION
SELECT * FROM t_order_01 WHERE user_name = "Hollis"
UNION
SELECT * FROM t_order_02 WHERE user_name = "Hollis"
UNION
SELECT * FROM t_order_03 WHERE user_name = "Hollis"
```





> 更新: 2024-07-08 12:11:42  
> 原文: <https://www.yuque.com/hollis666/dr9x5m/fz0atxiyv0obuwtd>