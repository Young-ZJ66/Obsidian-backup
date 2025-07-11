# ✅Redis 的分布式锁和 Zookeeper 的分布式锁有啥区别？

# 典型回答


在分布式锁的实现方案中，通常就是数据库、Redis 以及 Zookeeper 这三种，关于分布式锁的多种实现方式及原理我们这里不展开了，文档中已经有很多了，大家可以搜索下即可。



![1720861240049-1e35dc63-03d7-4794-ac11-a216ffa495b0.png](./img/aeYMZqkwbmQc_gV1/1720861240049-1e35dc63-03d7-4794-ac11-a216ffa495b0-009124.png)



本文主要聚焦 Redis 的分布式锁和Zookeeper 的分布式锁之间的区别，以及如何选择。



其实在功能上，Redis 的分布式锁和 ZK 的分布式锁都能实现我们想要的功能，锁的互斥、重入等等。他们主要有以下几个区别：



### 性能区别


在性能方面，Redis 是基于内存存储的，而 ZK 是基于磁盘存储的，所以，在性能上，Redis 要比 ZK 更好一些。





### 自动释放


ZK 的锁的实现原理是基于客户端和服务端的连接来保证的，一旦连接断了，锁就会被自动释放。而 Redis 的锁是需要自己主动加锁和解锁的，除非达到了超时时间，否则不会自动释放。



所以，ZK 的分布式锁可以更好的应对客户端崩溃的情况，一旦客户端崩溃，锁就会释放，而 Redis 实现的分布式锁，一旦客户端崩溃了，就没有人去进行释放了，只能等超时。



锁能自动释放有啥好处？除了提升并发度意外，还有个好处就是可以减少死锁发生的概率。因为锁释放了，所以就不会出现死锁了。



### 一致性&可用性要求（CAP）


我们分别介绍过关于 Redis和 Zookeeper 的 CAP 的实现情况，我们知道ZK 是一个 CP 的系统，也就是他是保证强一致性的，而 Redis 是一个 AP 的系统，它是保证可用性的。



[✅Zookeeper是CP的还是AP的？](https://www.yuque.com/hollis666/dr9x5m/lxznb86av97adwt6)



[✅Redis是AP的还是CP的？](https://www.yuque.com/hollis666/dr9x5m/uwx1gops5gfdv9wu)



**ZK 会牺牲可用性来保证数据的一致性**，即出现部分节点宕机后，集群中少于一半的节点后，或者集群正在进行 master 选举是，都会拒绝新的写请求，导致无法加锁。



而 **Redis 会牺牲一致性性来保证可用性**，即 Redis 的集群中在做数据同步时，如果出现网络延迟，那么即使多个节点上面的数据不一样，客户端也可以正常的进行写入和读取。



那么，在使用 ZK 的分布式锁的时候，不会存在锁丢失的情况，也就是说不太会出现因为锁丢失而导致并发的情况。但是，可能会出现短暂的无法加锁的情况。



而在使用 Redis 的分布式锁的时候，除非集群都挂了，要不然不太会出现无法加锁的情况。但是可能会出现锁丢失的情况，或者说是重复加锁的情况，我们介绍 RedLock 的时候提到的单点故障的问题：



[✅什么是RedLock，他解决了什么问题？](https://www.yuque.com/hollis666/dr9x5m/lxzg0ubs2xpvenxw)





### 做个总结


**Redis 实现的分布式锁、性能更好，可用性更高。ZK 实现的分布式锁可以自动释放，减少死锁出现的概率，并且他的一致性更有保障。**



所以，**如果你的分布式锁使用场景，对性能要求更高，可以牺牲一点一致性，那么就选择 Redis的分布式锁。而如果你的场景对性能要求没那么高，但是对一致性要求非常高，那么则可以选择 Zookeeper。**



### But


凡事都有个 but，下面就是一些经验之谈了。



其实，如果你对可用性的要求高的话，用 Redis 也行，因为有个 RedLock，他的机制和 zk 很像，都是通过半数以上提交这种方式来避免因为单点问题而导致锁重复的。（链接前面贴过了，这不再重复贴了）



但是，<font style="background-color:#FBDE28;">RedLock 其实我也不建议大家用，并且 ZK的分布式锁我其实也不建议大家用。就直接用 Redis 就好了。</font>



为啥呢？因为一般来说，我们在用分布式锁的时候，对性能要求肯定很高的，如果不高的话，你直接用数据库的悲观锁就好了。没必要用分布式锁。



而且，往往我们在用分布式锁的时候，同时会伴随着幂等性判断、以及数据库兜底的唯一性约束的校验。所以，即使出现了极端情况，因为 Redis 的一致性没保证好，导致重复加锁了，我们也能在后续的环节中识别并防止并发。



而 Redis 的不可用的问题其实可以通过哨兵、集群等运维手段来解决的，所以，发生的概率本来就极低。所以说，日常开发的时候，只要我们把幂等判断、唯一性约束做好，对账最好，用 Redis 是最简单，高效的办法。



而且，Redis 作为一个缓存框架，很多应用都会直接依赖，直接用SETNX 或者 Redisson 加锁不要太方便。而 Zookeeper，很多都是中间件在使用他， 真正的业务应用依赖的很少的，多引入一个底层中间件，对系统来说也会提升复杂度，减少整体的稳定性的。



除非你真的完全接受不了不一致性，完全不能接受重复加锁，有很愿意依赖 zookeeper，那当我没说，我认为这种情况少之又少。







> 更新: 2024-07-16 13:47:16  
> 原文: <https://www.yuque.com/hollis666/dr9x5m/wa9oz7l84ylazz58>