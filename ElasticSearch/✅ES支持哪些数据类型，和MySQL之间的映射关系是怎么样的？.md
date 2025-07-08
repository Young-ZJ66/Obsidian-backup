# ✅ES支持哪些数据类型，和MySQL之间的映射关系是怎么样的？

# 典型回答


<font style="color:rgb(13, 13, 13);">Elasticsearch支持以下数据类型</font>

<font style="color:rgb(13, 13, 13);"></font>

1. **Text**: 用于存储全文文本数据，如文章或书籍内容。支持全文搜索和分析。
2. **Keyword**: 用于存储文本值，通常用于索引结构化内容，如邮件地址、标签或任何需要精确匹配的内容。
3. **Date**: 存储日期或日期和时间。
4. **Long, Integer, Short, Byte, Double, Float**: 这些是数值类型，用于存储各种形式的数字。
5. **Boolean**: 存储 true 或 false 值。
6. **Binary**: 用于存储二进制数据。
7. **Object**: 用于嵌套文档，即文档内部可以包含文档。
8. **Nested**: 类似于 Object 类型，但用于存储数组列表，其中列表中的每个元素都是完全独立且可搜索的。



我们经常会把MySQL 中的数据同步到 ES 中，他们之间的类型的映射关系如下：



| **MySQL 类型** | **Elasticsearch 类型** | **说明** |
| :--- | :--- | :--- |
| <font style="color:rgb(13, 13, 13);">VARCHAR</font> | <font style="color:rgb(13, 13, 13);">text, keyword</font> | <font style="color:rgb(13, 13, 13);">根据是否需要全文搜索或精确搜索选择使用 text 或 keyword。</font> |
| <font style="color:rgb(13, 13, 13);">CHAR</font> | <font style="color:rgb(13, 13, 13);">keyword</font> | <font style="color:rgb(13, 13, 13);">通常映射为 keyword，因为它们用于存储较短的、不经常变化的字符序列。</font> |
| <font style="color:rgb(13, 13, 13);">BLOB/TEXT</font> | <font style="color:rgb(13, 13, 13);">text</font> | <font style="color:rgb(13, 13, 13);">大文本块使用 text 类型，支持全文检索。</font> |
| <font style="color:rgb(13, 13, 13);">INT, BIGINT</font> | <font style="color:rgb(13, 13, 13);">long</font> | <font style="color:rgb(13, 13, 13);">大多数整数类型映射为 long，以支持更大的数值。</font> |
| <font style="color:rgb(13, 13, 13);">TINYINT</font> | <font style="color:rgb(13, 13, 13);">byte</font> | <font style="color:rgb(13, 13, 13);">较小的整数可以映射为 byte 类型。</font> |
| <font style="color:rgb(13, 13, 13);">DECIMAL, FLOAT, DOUBLE</font> | <font style="color:rgb(13, 13, 13);">double, float</font> | <font style="color:rgb(13, 13, 13);">根据精确度需求选择 double 或 float。</font> |
| <font style="color:rgb(13, 13, 13);">DATE, DATETIME, TIMESTAMP</font> | <font style="color:rgb(13, 13, 13);">date</font> | <font style="color:rgb(13, 13, 13);">所有的日期时间类型均可映射为 date。</font> |
| <font style="color:rgb(13, 13, 13);">TINYINT(1)</font> | <font style="color:rgb(13, 13, 13);">boolean</font> | <font style="color:rgb(13, 13, 13);"></font> |




# 扩展知识


## <font style="color:rgb(13, 13, 13);">text 和 keyword 有啥区别？</font>


**text 类型被设计用于全文搜索**。这意味着当文本被存储为 text 类型时，Elasticsearch 会对其进行**分词**，把文本分解成单独的词或短语，便于搜索引擎进行全文搜索。**因为 text 字段经过分词，它不适合用于排序或聚合查询。**

****

**text适用于存储需要进行全文搜索的内容，比如新闻文章、产品描述等。**

****

**keyword 类型用于精确值匹配，不进行分词处理**。这意味着存储在 keyword 字段的文本会被当作一个完整不可分割的单元进行处理。**因为 keyword 类型字段是作为整体存储，它们非常适合用于聚合（如计数、求和、过滤唯一值等）和排序操作。**由于不进行分词，keyword 类型字段不支持全文搜索，但可以进行精确匹配查询。



**keyword适用于需要进行精确搜索的场景，比如标签、ID 编号、邮箱地址等。**  






> 更新: 2024-07-08 12:10:58  
> 原文: <https://www.yuque.com/hollis666/dr9x5m/neoehwlpx3yeeg7m>