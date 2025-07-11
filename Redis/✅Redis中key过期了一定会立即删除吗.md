# ✅Redis中key过期了一定会立即删除吗

# 典型回答


我们都知道，Redis的Key是可以设置过期时间的，那么，过期了一定会立即删除吗？



回答这个问题之前，我们先看下Redis是如何实现的Key的过期。



以下是官网中关于过期的实现的描述（[https://redis.io/commands/expire/](https://redis.io/commands/expire/) ）：

![1693564662579-2c439295-24af-4cad-ae5e-c4793f68deaf.png](./img/Ek-dKroMnTvB8hIx/1693564662579-2c439295-24af-4cad-ae5e-c4793f68deaf-539080.png)



也就是说Redis的键有两种过期方式：一种是被动过期，另一种是主动过期。

被动过期指的是当某个客户端尝试访问一个键，发现该键已经超时，那么它会被从Redis中删除。



当然，仅仅依靠被动过期还不够，因为有些过期的键可能永远不会再被访问。这些键应该被及时删除，因此Redis会定期随机检查一些带有过期时间的键。所有已经过期的键都会从键空间中删除。



具体来说，Redis每秒会执行以下操作10次：

1. 从带有过期时间的键集合中随机选择20个键。
2. 删除所有已经过期的键。
3. 如果已经过期的键占比超过25%，则重新从步骤1开始。



直到过期Key的比例下降到 25% 或者这次任务的执行耗时超过了25毫秒，才会退出循环

<font style="color:rgb(77, 77, 77);"></font>

所以，Redis其实是并不保证Key在过期的时候就能被立即删除的。因为一方面惰性删除中需要下次访问才会删除，即使是主动删除，也是通过轮询的方式来实现的。如果要过期的key很多的话，就会带来延迟的情况。





# 扩展知识


## 主动删除 vs 被动删除


主动删除的优点：

1. **及时释放内存**：主动删除能够及时地释放过期键占用的内存，避免内存空间被长时间占用，从而降低了内存使用率。
2. **避免写操作延迟**：由于过期键被定期删除，不会导致过多的过期键在访问时触发删除操作，因此可以减少读写操作的延迟。

主动删除的缺点：

1. **增加系统开销**：定期扫描和删除操作会增加系统的开销，特别是在有大量键需要处理时，可能会导致Redis的性能下降。



被动删除的优点：

1. **减少系统开销**：被动删除不会定期地进行扫描和删除操作，因此可以减少系统的开销，节省计算资源。

被动删除的缺点：

1. **可能导致内存占用高**：被动删除可能导致过期键长时间占用内存，直到被访问时才被删除，这可能会导致内存占用率较高。
2. **可能导致访问延迟**：当大量键同时过期并在访问时触发删除操作时，可能会导致读写操作的延迟。





**Redis的被动删除策略**，不需要额外配置。当你设置键的过期时间（TTL）时，Redis会自动处理被动删除。



要使用主动删除策略，需要在Redis配置文件中设置过期键检查的频率。你可以通过设置以下配置参数来调整主动删除的行为：

+ hz（每秒执行的定时器频率）：增加该值可以提高主动删除的频率。
+ maxmemory（Redis的最大内存限制）：设置合适的最大内存限制，以确保Redis在内存不足时触发主动删除。



例如，在Redis配置文件中可以设置：



```java
maxmemory 1gb
hz 10
```



> 更新: 2024-07-08 12:12:03  
> 原文: <https://www.yuque.com/hollis666/dr9x5m/ds8qgg4zmt7l2kvp>