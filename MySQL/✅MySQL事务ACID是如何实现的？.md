# ✅MySQL事务ACID是如何实现的？

# 典型回答


所谓ACID，其实是原子性、一致性、隔离性、持久性，那么，MySQL的事务是如何实现原子性、一致性、隔离性和持久性的呢？



### 原子性


原子性意味着事务的所有操作要么全部提交成功，要么全部失败回滚。MySQL的原子性是通过undolog实现的。



**Undo Log则用于在事务回滚或系统崩溃时撤销（回滚）事务所做的修改。**当一个事务执行过程中，MySQL会将事务<u>修改前</u>的数据记录到Undo Log中。如果事务需要回滚，则会从Undo Log中找到相应的记录来撤销事务所做的修改。



[✅binlog、redolog和undolog区别？](https://www.yuque.com/hollis666/dr9x5m/tdlgfm)





### 隔离性


隔离性指的是多个并发事务执行时，彼此互不干扰。MySQL的隔离性主要靠MVCC和锁机制来保证的。



我们都知道，MySQL中是有不同的隔离级别的，比如RC、RR等，这些的背后其实都是MVCC和锁在起作用。



在下面这篇中，我们介绍过，不同的隔离级别是分别如何实现的。



[✅InnoDB如何解决脏读、不可重复读和幻读的？](https://www.yuque.com/hollis666/dr9x5m/zx47wieewckee8bk)



| **隔离级别** | **实现方式** |
| --- | --- |
| **<font style="color:rgb(64, 64, 64);">读未提交</font>** | <font style="color:rgb(64, 64, 64);">直接读取最新数据，无锁和 MVCC 控制。</font> |
| **<font style="color:rgb(64, 64, 64);">读已提交</font>** | <font style="color:rgb(64, 64, 64);">每次查询生成新 ReadView，读取已提交的最新版本。</font> |
| **<font style="color:rgb(64, 64, 64);">可重复读</font>** | <font style="color:rgb(64, 64, 64);">事务开始时生成 ReadView，后续所有读操作基于此视图。</font> |
| **<font style="color:rgb(64, 64, 64);">串行化</font>** | <font style="color:rgb(64, 64, 64);">强制加锁，所有操作串行执行。</font> |




### **<font style="color:rgb(64, 64, 64);">持久性</font>**


持久性指的是事务提交后，修改永久保存，即使系统崩溃也不丢失。



这个我认为主要是依赖MySQL的持久化机制，它是基于磁盘存储的，并且还有Redo Log可以用来崩溃恢复。



[✅binlog、redolog和undolog区别？](https://www.yuque.com/hollis666/dr9x5m/tdlgfm)



**Redo Log是MySQL用于实现崩溃恢复和数据持久性的一种机制。**在事务进行过程中，MySQL会将事务<u>做了什么改动</u>到Redo Log中。当系统崩溃或者发生异常情况时，MySQL会利用Redo Log中的记录信息来进行恢复操作，将事务所做的修改持久化到磁盘中。



### 一致性


一致性，要求事务执行后，数据库从一个一致状态转换到另一个一致状态。



MySQL中还有很多主键、外键、唯一性约束、非空约束等等都能帮我们保证数据的一致性的逻辑。还有就是其实一致性最重视靠底层 ACID 机制共同保障的，如果原子性、隔离性、持久性做到了，那一致性也就满足了。



[✅什么是事务的2阶段提交？](https://www.yuque.com/hollis666/dr9x5m/geuks1bbiwd39h1r)





### 总结
| **特性** | **实现机制** |
| --- | --- |
| **<font style="color:rgb(64, 64, 64);">原子性</font>** | <font style="color:rgb(64, 64, 64);">Undo Log</font> |
| **<font style="color:rgb(64, 64, 64);">隔离性</font>** | <font style="color:rgb(64, 64, 64);">锁机制（共享锁、排他锁、间隙锁） + MVCC（版本链、ReadView）</font> |
| **<font style="color:rgb(64, 64, 64);">持久性</font>** | <font style="color:rgb(64, 64, 64);">Redo Log（崩溃恢复）</font> |
| **<font style="color:rgb(64, 64, 64);">一致性</font>** | <font style="color:rgb(64, 64, 64);">原子性、隔离性、持久性共同保障 + 数据库约束</font> |




> 更新: 2025-03-08 14:39:27  
> 原文: <https://www.yuque.com/hollis666/dr9x5m/opw12171lnkklux0>