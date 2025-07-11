# ✅MySQL的深度分页如何优化

# 典型回答


深度分页问题是指在数据库查询中，当你尝试访问通过分页查询返回的结果集的后面部分（即深层页码）时遇到的性能问题。



假设你有一个包含数百万条记录的表，你想通过分页的方式来展示这些数据。当用户请求第10000页数据时，假设pageSize为10，那么最终就是LIMIT 99990,10 ，数据库必须先扫描过前99990条记录，才能返回第10000页的数据，这会导致显著的性能下降。



> 99991是起始ID = (页数 - 1) * 每页项目数 + 1 
>
> 对于第1页，起始ID将是1，结束ID将是10。对于第2页，起始ID将是11，结束ID将是20，以此类推。
>
> 对于第10000页：
>
> 起始ID = (10000 - 1) * 10 + 1 = 99991
>



深度分页的问题想要优化，有以下几个手段。



### 使用子查询和JOIN优化


假如我们这样一条SQL：



```latex
SELECT c1, c2, cn... FROM table WHERE name = "Hollis" LIMIT 1000000,10
```



我们可以基于子查询进行优化，如以下SQL：



```latex
SELECT c1, c2, cn...
FROM table
INNER JOIN (
    SELECT id
    FROM table
    WHERE name = "Hollis"
    ORDER BY id
    LIMIT 1000000, 10
) AS subquery ON table.id = subquery.id

```



首先，使用一个子查询来获取限定条件下的一小部分主键id，这部分 id 对应于我们分页的目标区域。然后，使用这些 id 在主查询中获取完整的行数据。



以上SQL，在name有索引的情况下，子查询中查询id是不需要回表的。而当我们查询出我们想要的10个ID之后，基于ID查询不仅快，而且要查的数据量也很少。





### 使用子查询和ID过滤优化


和上面的方法类似，我们还可以把SQL优化成：



```latex
SELECT c1, c2, cn...
FROM table
WHERE name = "Hollis"
  AND id >= (SELECT id FROM table WHERE name = "Hollis" ORDER BY id LIMIT 1000000, 1)
ORDER BY id
LIMIT 10

```





这个方法代替了join的方式，使用了一个子查询来获取从哪里开始分页的参考点，基于ID做范围查询。但是这个方案有个弊端，那就是要求ID一定要是自增的。



和上面的方案同理，他也可以减少回表的次数。



### 记录上一个ID


还有一种方式，是上面这个方式的变种，就是如果能提前预估要查询的分页的条件的话，是可以很大程度提升性能的。比如记住上一页的最大ID，下一页查询的时候，就可以可以根据id >　max_id_in_last_page 进行查询。





### 使用搜索引擎


另外，如果是基于文本内容的搜索，可以使用 Elasticsearch 这样的全文搜索引擎来优化深度分页性能。但是需要注意的是，ES也会有深度分页的问题，只不过他的影响比MySQL要小一些。





> 更新: 2024-07-19 21:17:20  
> 原文: <https://www.yuque.com/hollis666/dr9x5m/et8lo7l10rg7g7iy>