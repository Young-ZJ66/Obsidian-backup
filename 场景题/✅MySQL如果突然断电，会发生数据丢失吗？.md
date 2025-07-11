# ✅MySQL如果突然断电，会发生数据丢失吗？

# 典型回答


**对于 InnoDB 存储引擎**，如果配置得当（如 `innodb_flush_log_at_trx_commit = 1`），大多数情况下，突然断电后数据不会丢失，MySQL 会通过事务日志进行恢复。只有 **未提交的事务** 会丢失。



> **<font style="color:rgb(25, 25, 25);">innodb_flush_log_at_trx_commit</font>**<font style="color:rgb(25, 25, 25);">：</font>
>
> + <font style="color:rgb(25, 25, 25);">0：日志缓存区将每隔一秒写到日志文件中，并且将日志文件的数据刷新到磁盘上。该模式下在事务提交时不会主动触发写入磁盘的操作。</font>
> + <font style="color:rgb(25, 25, 25);">1：每次事务提交时MySQL都会把日志缓存区的数据写入日志文件中，并且刷新到磁盘中，该模式为系统默认的。</font>
> + <font style="color:rgb(25, 25, 25);">2：每次事务提交时MySQL都会把日志缓存区的数据写入日志文件中，但是并不会同时刷新到磁盘上。该模式下，MySQL会每秒执行一次刷新磁盘操作。</font>
>



**对于 MyISAM 存储引擎**，断电可能导致表损坏或数据丢失，因为它没有事务日志机制。



如果使用了不当的磁盘缓存设置、较低的 `innodb_flush_log_at_trx_commit` 配置值或没有开启 `sync_binlog`，则可能会丢失一些数据。



但是大家需要注意！！！**<u>现代操作系统和硬件通常会对磁盘进行缓存，这意味着在写入磁盘时，数据可能会先被写入操作系统的缓存中，而不是直接写入磁盘。如果在缓存未刷新到磁盘时断电，这部分数据可能会丢失。为了避免这种情况，可以通过关闭磁盘缓存或者使用专用的硬件来减少风险。  </u>**

# 扩展知识


## Innodb的事务日志


MySQL 使用了 **InnoDB** 存储引擎时，所有的数据更改操作都会被记录在**redo log**中。这些事务日志是为了保证事务的原子性和持久性（ACID）而设计的。如果数据库突然断电，InnoDB 通过事务日志来确保数据的一致性和持久性，尽量避免数据丢失。  （这个过程其实就是崩溃恢复）



Innodb的所有事务操作都会先写入 redo log，而不是直接写入数据文件。而且MySQL 还会记录 **binlog**，它用于复制和恢复数据。详见：

  

[✅什么是事务的2阶段提交？](https://www.yuque.com/hollis666/dr9x5m/geuks1bbiwd39h1r)



**如果发生断电**，对于已提交的事务，MySQL 会通过 redo log 恢复已提交的事务，因此已经提交的数据不会丢失。而对于未提交的事务，MySQL 会在重启后回滚这些事务，这意味着这些未提交的数据会丢失。



## UPS


在很多公司中，为了避免意外断电带来的风险，通常会部署 **不间断电源（UPS）**，这可以在断电时为服务器提供足够的时间来完成数据写入并安全关闭。通过硬件冗余和 UPS 系统，可以在断电时提高数据的持久性和安全性。  



> 更新: 2025-01-12 13:41:31  
> 原文: <https://www.yuque.com/hollis666/dr9x5m/nxtpavyryigig9q9>