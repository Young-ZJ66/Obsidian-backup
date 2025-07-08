# ✅InnoDB和MyISAM有什么区别？

# 典型回答


InnoDB和MyISAM是MySQL中比较常用的两个执行引擎，<font style="color:rgb(51, 51, 51);">MySQL 在 5.5 之前版本默认存储引擎是 MyISAM，5.5 之后版本默认存储引擎是 InnoDB，MyISAM适合查询以及插入为主的应用，InnoDB适合频繁修改以及涉及到安全性较高的应用。</font>



> + 如果应用需要高度的数据完整性和事务支持，那么InnoDB是更好的选择。所以频繁修改及数据安全性的情况适合。
> + 如果应用主要是读取操作，或者需要高效的全文搜索功能，那么MyISAM可能更适合。所以查询频繁的适合。
>



他们主要有以下区别：



+ <font style="color:rgb(51, 51, 51);">一、</font>**<font style="color:rgb(51, 51, 51);">InnoDB支持事务</font>**<font style="color:rgb(51, 51, 51);">，MyISAM不支持</font>
+ <font style="color:rgb(18, 18, 18);">二、</font>**<font style="color:rgb(18, 18, 18);">InnoDB 是聚集索引</font>**<font style="color:rgb(18, 18, 18);">，MyISAM 是非聚集索引。MyISAM是采用了一种索引和数据分离的存储方式，Innodb的聚簇索引中索引和数据在一起。</font>
+ <font style="color:rgb(51, 51, 51);">三、</font>**<font style="color:rgb(51, 51, 51);">InnoDB支持外键</font>**<font style="color:rgb(51, 51, 51);">，MyISAM不支持</font>
+ <font style="color:rgb(18, 18, 18);">四、</font>**<font style="color:rgb(18, 18, 18);">InnoDB 最小的锁粒度是行锁</font>**<font style="color:rgb(18, 18, 18);">，MyISAM 最小的锁粒度是表锁。</font>
+ <font style="color:rgb(51, 51, 51);">五、</font>**<font style="color:rgb(51, 51, 51);">InnoDB不支持FULLTEXT类型的索引（5.6之前不支持全文索引）</font>**
+ <font style="color:rgb(51, 51, 51);">六、</font>**<font style="color:rgb(51, 51, 51);">InnoDB中不保存表的行数</font>**<font style="color:rgb(51, 51, 51);">，但是MyISAM只要简单的读出保存好的行数即可</font>
+ <font style="color:rgb(51, 51, 51);">七、对于自增长的字段，InnoDB中必须包含只有该字段的索引，但是在MyISAM表中可以和其他字段一起建立联合索引</font>

<font style="color:rgb(51, 51, 51);"></font>

| **** | **InnoDB** | **MyISAM** |
| --- | --- | --- |
| **事务** | 支持 | 不支持 |
| **外键** | 支持 | 不支持 |
| **聚簇索引** | 支持 | 不支持 |
| **锁级别** | 支持行级锁、表级锁 | 表级锁 |
| **行数保存** | 不支持 | 支持 |
| **默认版本** | <font style="color:rgb(51, 51, 51);">5.5 之后</font> | <font style="color:rgb(51, 51, 51);">5.5 之前</font> |
| **全文索引** | 5.6以后支持 | 支持 |


<font style="color:rgb(51, 51, 51);"></font>

# <font style="color:rgb(51, 51, 51);">扩展知识</font>


## 索引结构区别


[✅MyISAM 的索引结构是怎么样的，它存在的问题是什么？](https://www.yuque.com/hollis666/dr9x5m/mcl4sn8mcutieesz)

  
 



> 更新: 2025-02-09 12:34:03  
> 原文: <https://www.yuque.com/hollis666/dr9x5m/adeg5m>