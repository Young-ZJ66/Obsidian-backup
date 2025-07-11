# ✅Oracle 和 MySQL 的区别是什么？如何选择？

# 典型回答


**Oracle是一个企业级数据库系统**，支持大规模应用、高并发和高可用性。它具有复杂的架构，支持多租户、多实例以及丰富的特性，如高级备份和恢复、安全管理、分布式数据库、数据仓库、物化视图等。



因为是收费的，所以**Oracle在性能优化、负载均衡和集群技术方面有很强的能力**。支持RAC（Real Application Clusters）等技术，可以实现高可用性和可扩展性。



还是因为收费，所以**Oracle有完善的商业支持和服务体系，提供全球性的技术支持和咨询服务，适合大企业的复杂业务需求。**



**MySQL是一个开源的数据库系统**，通常用于中小型应用或作为Web应用的后端数据库。它的架构相对简单，易于部署和管理。MySQL更注重读操作性能，适合高读取量的应用。



因为是开源的，所以 MySQL 相比 Oracle有更广泛的社区支持，也有企业版提供商业支持，但其支持服务肯定是不如 Oracle的。



另外，一些其他的区别如下（每一个具体的内容我们会在其他文章中展开）：



| **** | **Oracle** | **MySQL** |
| --- | --- | --- |
| **定位** | 企业级数据库 | 开源数据库 |
| **默认事务隔离级别** | RC | RR |
| **执行引擎** | 只有一种引擎 | <font style="color:rgb(13, 13, 13);">支持多种存储引擎</font> |
| **SQL语法** | 支持 PL/SQL，支持存储过程、触发器等 | 支持标准 SQL |
| **事务提交** | 默认不自动提交，需要手动提交 | 默认自动提交 |
| **主键** | <font style="color:rgb(51, 51, 51);">序列号</font> | <font style="color:rgb(37, 41, 51);">auto increment</font> |
| **分页** | ROWNUM 或者 ROW_NUMBER() | <font style="color:rgb(37, 41, 51);"> limit</font> |
| **索引** | B+ 树、位图、反向键、函数索引、域索引 | B+树、全文、哈希索引 |
| **数据恢复** | <font style="color:rgb(51, 51, 51);">RAC</font> | <font style="color:rgb(51, 51, 51);">主从复制</font> |
| **字符串连接** | `<font style="color:rgb(51, 51, 51);">||</font>`<font style="color:rgb(51, 51, 51);">运算符</font> | CONCAT函数 |
| **其他** | <font style="color:rgb(51, 51, 51);">...</font> | ... |




> 更新: 2024-07-08 12:11:58  
> 原文: <https://www.yuque.com/hollis666/dr9x5m/hrdea48tzqmtizbk>