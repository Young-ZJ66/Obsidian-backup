# ✅Redis保存库存的时候，如何避免被Redis清理掉？

# 典型回答


用Redis做库存扣减，是非常常见的一种抗高并发的方案。但是，如何避免这个库存被Redis给清理掉呢？**这其实是一个关于Redis的淘汰策略的问题。**

****

[✅Redis的内存淘汰策略是怎么样的？](https://www.yuque.com/hollis666/dr9x5m/xw99lcraocebx1mk)



上面这篇文章介绍过，Redis的淘汰策略分几种，比如lru、lfu、random等等，不管是哪种，其实太还会有另外一个叠加条件，那就是allkeys还是volatile



allkeys就是所有的key都参数LFU、LFU等等的淘汰筛选。而volatile则是只有设置了超时时间的key才会参与到淘汰筛选中。



一般来说，allkeys-lru和volatile-lru用的比较多，allkeys这种主要用于你把Redis当纯缓存的时候，就是他没了就没了，无所谓。大不了去查数据库。



而Redis来做库存处理，是一种非常典型的半缓存半持久化的场景，这种场景就比较适合volatile-lru这种策略，这也是像阿里云上的Redis的默认的淘汰策略。



当然，如果你为了保险，你可以像腾讯云的redis一样，选择noeviction作为淘汰策略，他在内存满了之后会OOM，而不是帮你淘汰数据。但是这种我不太建议，因为内存毕竟有限，还是设置个淘汰策略好一点。



> 更新: 2025-02-26 22:15:09  
> 原文: <https://www.yuque.com/hollis666/dr9x5m/fwh7tsxgyr63c43w>