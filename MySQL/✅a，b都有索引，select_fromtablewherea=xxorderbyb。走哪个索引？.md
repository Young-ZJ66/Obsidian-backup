# ✅a，b都有索引，select * from table where a = xx order by b。走哪个索引？

# 典型回答


不一定。有可能走a的索引，有可能走b的索引。



[✅为什么MySQL会选错索引，如何解决？](https://www.yuque.com/hollis666/dr9x5m/ghy5i20ie717exee)



在上面的文章介绍过，mysql选择索引的时候，有很多考量，包括了基数性、选择性、order by等。优化器会根据成本预估选择一个他认为合适的索引。



如果 `WHERE a = xx` 的过滤条件的选择性较高（即能过滤掉大量行），MySQL 可能优先使用 `a` 的索引来快速定位满足条件的记录。  



如果 `WHERE a = xx` 的过滤条件的选择性较低（即 `a = xx` 会匹配大量的记录），而 `ORDER BY b` 对结果的顺序要求较高，MySQL 可能使用 `b` 的索引来避免排序操作。  



> 更新: 2024-12-21 12:59:16  
> 原文: <https://www.yuque.com/hollis666/dr9x5m/sopm64dgvu5g2m5h>