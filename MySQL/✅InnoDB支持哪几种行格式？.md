# ✅InnoDB支持哪几种行格式？

# 典型回答


数据库表的行格式决定了一行数据是如何进行物理存储的，进而影响查询和DML操作的性能。



在InnoDB中，常见的行格式有4种：



1. **COMPACT** ：是MySQL 5.0之前的默认格式，除了保存字段值外，还会利用空值列表保存null值，还会记录变长字段长度列表和记录头信息。



![1691226687920-9b65a97a-4cc8-4f19-89d3-4cf8f099c059.png](./img/uDRss6aD_peebx6t/1691226687920-9b65a97a-4cc8-4f19-89d3-4cf8f099c059-796652.png)



COMPACT 适合处理大量包含可变长度列（如VARCHAR、VARBINARY、BLOB和TEXT类型）的数据。



> 对于可变长度列，前768字节的数据存储在B树节点的索引记录中，超出部分存储在溢出页中。大于或等于768字节的固定长度列会被编码为可变长度列，并可以存储在页外。
>



2. **REDUNDANT** ：Redundant 是 MySQL5.0 版本之前 InnoDB 的行记录存储方式，用的比较少，Redundant 行格式会把该条记录中所有列 (包括隐藏列) 的长度信息都存储到 '字段长度偏移列表' 中。





![1691226921724-f2365ad2-beb2-458a-962d-b3d8ffc40a78.png](./img/uDRss6aD_peebx6t/1691226921724-f2365ad2-beb2-458a-962d-b3d8ffc40a78-359177.png)





3. **DYNAMIC**：DYNAMIC格式在MySQL 5.7版本引入，是COMPACT格式的改进版。它保持了COMPACT格式的优点，同时在存储大的可变长度列时更加灵活，能够动态地选择存储在页内或页外。DYNAMIC格式适用于大部分的应用场景，并在存储空间和性能上做了一定的平衡。其结构和COMPACT大致相同；



4. **COMPRESSED**：是MySQL 5.1中InnoDB的新特性之一，它可以在存储数据时对数据进行压缩，从而减小磁盘占用空间。它的缺点是增加了CPU的使用，可能会降低一些查询的性能。COMPRESSED 行格式是在 DYNAMIC 行格式的基础上添加了页外压缩功能。在存储时，如果发现数据可以通过压缩减小存储空间，就会使用压缩方式来存储数据。在查询时，会自动解压缩数据并返回结果。





| **<font style="color:rgb(36, 41, 46);">行格式</font>** | **<font style="color:rgb(36, 41, 46);">紧凑的存储特性</font>** | **<font style="color:rgb(36, 41, 46);">增强的可变长度列存储</font>** | **<font style="color:rgb(36, 41, 46);">大索引键前缀支持</font>** | **<font style="color:rgb(36, 41, 46);">压缩支持</font>** | **<font style="color:rgb(36, 41, 46);">支持的表空间类型</font>** | **<font style="color:rgb(36, 41, 46);">所需文件格式</font>** |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| <font style="color:rgb(36, 41, 46);">REDUNDANT</font> | <font style="color:rgb(36, 41, 46);">否</font> | <font style="color:rgb(36, 41, 46);">否</font> | <font style="color:rgb(36, 41, 46);">否</font> | <font style="color:rgb(36, 41, 46);">否</font> | <font style="color:rgb(36, 41, 46);">system, file-per-table, general</font> | <font style="color:rgb(36, 41, 46);">Antelope or Barracuda</font> |
| <font style="color:rgb(36, 41, 46);">COMPACT</font> | <font style="color:rgb(36, 41, 46);">是</font> | <font style="color:rgb(36, 41, 46);">否</font> | <font style="color:rgb(36, 41, 46);">否</font> | <font style="color:rgb(36, 41, 46);">否</font> | <font style="color:rgb(36, 41, 46);">system, file-per-table, general</font> | <font style="color:rgb(36, 41, 46);">Antelope or Barracuda</font> |
| <font style="color:rgb(36, 41, 46);">DYNAMIC</font> | <font style="color:rgb(36, 41, 46);">是</font> | <font style="color:rgb(36, 41, 46);">是</font> | <font style="color:rgb(36, 41, 46);">是</font> | <font style="color:rgb(36, 41, 46);">否</font> | <font style="color:rgb(36, 41, 46);">system, file-per-table, general</font> | <font style="color:rgb(36, 41, 46);">Barracuda</font> |
| <font style="color:rgb(36, 41, 46);">COMPRESSED</font> | <font style="color:rgb(36, 41, 46);">是</font> | <font style="color:rgb(36, 41, 46);">是</font> | <font style="color:rgb(36, 41, 46);">是</font> | <font style="color:rgb(36, 41, 46);">是</font> | <font style="color:rgb(36, 41, 46);">file-per-table, general</font> | <font style="color:rgb(36, 41, 46);">Barracuda</font> |




> 更新: 2024-07-08 12:11:46  
> 原文: <https://www.yuque.com/hollis666/dr9x5m/git053kfd3r0fc8o>