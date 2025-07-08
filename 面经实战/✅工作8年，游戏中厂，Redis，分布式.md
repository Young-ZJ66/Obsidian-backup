# ✅工作8年，游戏中厂，Redis，分布式

# 面试者背景




:::warning
**8年，中厂游戏，Java，go，spring，做过dbserver，游戏饰品商城（交易模块、第三方支付接入），压测系统（xml、protobuf、流程化配置、分布式压测，Prometheus、grafana），**

**如何实现的压测的并发数，场景化配置是如何实现的？作弊指令，**

**压测时关注哪些指标？****p90****大概多少****ms****？****100ms**

**游戏账号是如何维护的？为啥不用开源的方案比如****jemeter****？**

**用过哪些中间件？****redis****、****mongodb****、****mq****、****mysql****。****redis****和****mongodb****区别？**

**Redis****什么地方用到了？**

**为啥****mysql****用****B+****树，****mongodb****为啥用****B****树，****redis****用跳表？**

**三种数据库该怎么选？一般是如何选择？**

**Redis****的事务和****mysql****的事务区别？**

**Redis****快的原因是什么？基于内存、单线程模型、多路复用，为啥单线程会更快？**

**Redis****的热****key****问题遇到过吗？有什么问题吗？多级缓存、拆分。本地缓存不一致问题怎么办？**

**热****key****变成了大****key****怎么办？你觉得多大可以认为是大****key****？**

**Redis****的分布式锁，如何实现可重入？什么是可重入？如何避免解锁的时候把别人的锁解了？听说过****redlock****吗？**

**Lua****脚本用过吗？在集群模式下使用****lua****脚本有问题么？有办法解决吗？**

**Zookeeper****干什么用了？为啥****zk****可以用来做****nameserver****？**

**Zookeeper****的****CP****体现在哪里？强一致性，查询的时候一定会不一样呢？不一致了怎么体现强一致性？****A****的牺牲体现在哪里？**

**写完****1/2****节点之后，如果超过****1/2****节点都挂了怎么办？**

**Zk****能用在什么场景下？****zk****的分布式锁和****redis****的分布式锁区别是啥？性能、原理、一致性、**

**分布式锁，一致性和可用性哪个更重要？为啥市面上****99%****场景都用****redis****？数据库兜底，**

**分布式事务涉及过吗？介绍下****TCC****，你认为有必要做分布式事务吗？太重了，**

**不做分布式事务，怎么保证一致性呢？**

**“为什么要限流，不应该服务好用户么？”，如何反驳？恶意流量、上下游**

:::

# 题目解析


:::color4
**如何实现的压测的并发数，场景化配置是如何实现的？作弊指令，**

**压测时关注哪些指标？p90大概多少ms？100ms**

:::



[✅说下什么是p90，p95，P99？](https://www.yuque.com/hollis666/dr9x5m/nz2cp6vbkexabpma)



:::color4
**用过哪些中间件？****redis****、****mongodb****、****mq****、****mysql****。****redis****和****mongodb****区别？**

**Redis****什么地方用到了？**

**为啥****mysql****用****B+****树，****mongodb****为啥用****B****树，****redis****用跳表？**

**三种数据库该怎么选？一般是如何选择？**

**Redis的事务和mysql的事务区别？**

:::



[✅Redis、MySQL和MongoDB的区别是什么，各自适用场景呢？](https://www.yuque.com/hollis666/dr9x5m/dip4hk9phfqepm8s)



[✅为什么MySQL用B+树，MongoDB用B树？](https://www.yuque.com/hollis666/dr9x5m/pp4wesnfc5w2smgg)



[✅InnoDB为什么不用跳表，Redis为什么不用B+树？](https://www.yuque.com/hollis666/dr9x5m/lcz0grveudyoa16b)



[✅Redis的事务和MySQL的事务区别？](https://www.yuque.com/hollis666/dr9x5m/xicgnpu302s7veme)



:::color4
**Redis****快的原因是什么？基于内存、单线程模型、多路复用，为啥单线程会更快？**

**Redis****的热****key****问题遇到过吗？有什么问题吗？多级缓存、拆分。本地缓存不一致问题怎么办？**

**热key变成了大key怎么办？你觉得多大可以认为是大key？**

:::



[✅Redis为什么这么快？](https://www.yuque.com/hollis666/dr9x5m/kc7dw3)



[✅什么是热Key问题，如何解决热key问题](https://www.yuque.com/hollis666/dr9x5m/lysd3t)



[✅什么是大Key问题，如何解决？](https://www.yuque.com/hollis666/dr9x5m/qiqc1r6r3catcev9)



:::color4
**Redis的分布式锁，如何实现可重入？什么是可重入？如何避免解锁的时候把别人的锁解了？听说过redlock吗？**

:::



[✅什么是可重入锁，怎么实现可重入锁？](https://www.yuque.com/hollis666/dr9x5m/zvx2w5h9sr7trle7)



[✅什么是RedLock，他解决了什么问题？](https://www.yuque.com/hollis666/dr9x5m/lxzg0ubs2xpvenxw)



:::color4
**Lua脚本用过吗？在集群模式下使用lua脚本有问题么？有办法解决吗？**

:::



[✅Redis Cluster 中使用事务和 lua 有什么限制？](https://www.yuque.com/hollis666/dr9x5m/zb66y7he56otikqs)



:::color4
**Zookeeper****干什么用了？为啥****zk****可以用来做****nameserver****？**

**Zookeeper****的****CP****体现在哪里？强一致性，查询的时候一定会不一样呢？不一致了怎么体现强一致性？****A****的牺牲体现在哪里？**

**写完****1/2****节点之后，如果超过****1/2****节点都挂了怎么办？**

**Zk能用在什么场景下？**

:::



[✅Zookeeper的典型应用场景有哪些？](https://www.yuque.com/hollis666/dr9x5m/bxldoz3kvfpdsv1g)



[✅Zookeeper是CP的还是AP的？](https://www.yuque.com/hollis666/dr9x5m/lxznb86av97adwt6)



:::color4
**zk的分布式锁和redis的分布式锁区别是啥？性能、原理、一致性、**

**分布式锁，一致性和可用性哪个更重要？为啥市面上99%场景都用redis？数据库兜底，**

:::





[✅Redis 的分布式锁和 Zookeeper 的分布式锁有啥区别？](https://www.yuque.com/hollis666/dr9x5m/wa9oz7l84ylazz58)





:::color4
**分布式事务涉及过吗？介绍下****TCC****，你认为有必要做分布式事务吗？太重了，**

**不做分布式事务，怎么保证一致性呢？**

:::



[✅什么是分布式事务？](https://www.yuque.com/hollis666/dr9x5m/pgzeqn8h4nxl1o6h)



[✅怎么做数据对账？](https://www.yuque.com/hollis666/dr9x5m/vh0msbr3qrqzfrfm)



:::color4
**“为什么要限流，不应该服务好用户么？”，如何反驳？恶意流量、上下游**

:::



[✅为什么一定要做限流？不应该服务好客户吗？不应该是加机器吗？](https://www.yuque.com/hollis666/dr9x5m/pfgbuemozdgl0m93)



> 更新: 2024-12-18 20:18:12  
> 原文: <https://www.yuque.com/hollis666/dr9x5m/cngc34qdie1pidv7>