# ✅有了关系型数据库，为什么还需要NOSQL？

# 典型回答


NOSQL数据库无需提前设计表结构，数据可以根据需要自由地存储和组织，而且相对于关系型数据库，NOSQL高效灵活，非常适合那些复杂、高变化、高并发量的场景中。



# 扩展知识


## <font style="color:rgb(36, 41, 47);">什么是关系型数据库，什么是非关系型数据库？</font>


<font style="color:rgb(36, 41, 47);">关系型数据库，是指采用了关系模型来组织数据的数据库（关系模型可以简单理解为二维表格模型），其以行和列的形式存储数据，以便于用户管理。</font>

<font style="color:rgb(36, 41, 47);"></font>

<font style="color:rgb(36, 41, 47);">关系型数据库中有表的概念，表中包含了行和列，多张（或1张）表可以组成数据库。</font>

<font style="color:rgb(36, 41, 47);"></font>

<font style="color:rgb(36, 41, 47);">关系型数据库具有以下几个特点：</font>

<font style="color:rgb(36, 41, 47);">1、传统的关系型数据库中的数据以行和列的方式进行存储。 </font>

<font style="color:rgb(36, 41, 47);">2、关系型数据库采用结构化查询语言（即SQL）来对数据库进行查询 </font>

<font style="color:rgb(36, 41, 47);">3、关系型数据库强调ACID规则（原子性（Atomicity）、一致性（Consistency）、隔离性（Isolation）、持久性（Durability）） </font>

<font style="color:rgb(36, 41, 47);">4、关系型数据库十分强调数据的一致性，并为此降低读写性能付出了巨大的代价 </font>

<font style="color:rgb(36, 41, 47);">5、关系型数据的数据通常存储在硬盘中</font>

<font style="color:rgb(36, 41, 47);"></font>

<font style="color:rgb(36, 41, 47);">我们常见的MySQL、Oracle等都是关系型数据库。但是因为关系型数据库强调强一致性、以及基于硬盘存储，所以存在着一定的性能问题，相比之下，非关系型数据库在这方面就会相对有些优势。</font>

<font style="color:rgb(36, 41, 47);"></font>

<font style="color:rgb(36, 41, 47);">NoSQL表示非关系型数据库，主要指那些非关系型的、分布式的，且一般不保证ACID的数据存储系统，主要代表如Redis、MongoDB等。</font>

<font style="color:rgb(36, 41, 47);"></font>

<font style="color:rgb(36, 41, 47);">非关系型数据库的存储方式是基于键值来存储的，对于值的类型也有不同的支持，所以没有固定的要求和限制。</font>

<font style="color:rgb(36, 41, 47);"></font>

## <font style="color:rgb(36, 41, 47);">关系型数据库和非关系型数据库主要有哪些区别？</font>


<font style="color:rgb(36, 41, 47);">1、关系型数据库以表的形式进行存储数据，而非关系型数据库以Key-value的形式存储数据。 </font>

<font style="color:rgb(36, 41, 47);">2、关系型数据库需要保证事务的ACID，而非关系型数据库中的事务一般无法回滚。（也有部分数据库可以回滚，如MongoDB在集群模式下） </font>

<font style="color:rgb(36, 41, 47);">3、关系型数据库可以通过一张表中的任意字段进行查询，非关系型数据库需要通过key进行查询 </font>

<font style="color:rgb(36, 41, 47);">4、一般来说，关系型数据库是基于硬盘存储，非关系型数据库基于内存存储。 （Mongodb基于磁盘存储）</font>

<font style="color:rgb(36, 41, 47);">5、关系型数据库支持各种范围查询、公式计算等，非关系型数据库不一定支持。</font>

  


  




> 更新: 2024-07-08 12:11:54  
> 原文: <https://www.yuque.com/hollis666/dr9x5m/ic65fs>