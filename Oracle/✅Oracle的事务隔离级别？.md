# ✅Oracle 的事务隔离级别？

# 典型回答
我们都知道，数据库是是支持多个事务同时执行的，而这些同时执行的事务能不能看到别的事务更高的数据呢？能看到哪些数据？这就是事务隔离级别来规定的。



所谓事务隔离级别，是数据库管理系统（DBMS）中用于定义**事务处理过程中不同事务之间可见性和相互影响程度**的一套标准。



事务隔离级别的主要目的是平衡数据的一致性和系统的并发性，一般来说更高的隔离级别虽然能提高数据的一致性，但同时也可能降低系统的并发能力。



在我们常用的 MySQL 中，支持可串行化(Serializable)、可重复读(Repeatable reads)、提交读(Read committed)、未提交读(Read uncommitted)这四种隔离级别。**而 Oracle ，只支持提交读(Read committed)和****<font style="color:rgb(13, 13, 13);">可串行化（Serializable），以及他自己定义的只读（Read Only）</font>**

**<font style="color:rgb(13, 13, 13);"></font>**

### 可读提交（Read Committed）
RC是Oracle的默认事务隔离级别。在此级别下，一个事务只能看到其他事务已经提交的更改。



这意味着，每次查询只能看到查询开始时已经提交的数据。这种隔离级别有效地防止了“脏读”，但无法防止“不可重复读”和“幻读”



[✅什么是脏读、幻读、不可重复读？](https://www.yuque.com/hollis666/dr9x5m/vp4vma02le3z3y50)



### 可串行化（Serializable）


这是一种非常严格的隔离级别，在此隔离级别下，事务将看到一致性的数据库快照，该快照从事务开始时刻起就不再改变。



这个级别可以防止脏读、不可重复读和幻读。



在Oracle中，可以使用`ALTER SESSION`命令来设置会话的隔离级别。例如，设置会话为可串行化：



```latex
ALTER SESSION SET ISOLATION_LEVEL=SERIALIZABLE;
```



### 只读（Read Only）


在只读隔离级别下，事务看到的是在事务开始时刻数据库的一个静态快照。该级别的事务不能执行任何更新操作（即DML语句如INSERT, UPDATE, DELETE），只能执行查询操作。



这个隔离级别同样可以防止脏读、不可重复读和幻读（只有读，没有写了，啥问题都没有了）。它适用于需要执行长时间运行的查询而不影响其他事务的场景。







> 更新: 2024-07-19 22:13:48  
> 原文: <https://www.yuque.com/hollis666/dr9x5m/uy74dk6ebd53wuhh>