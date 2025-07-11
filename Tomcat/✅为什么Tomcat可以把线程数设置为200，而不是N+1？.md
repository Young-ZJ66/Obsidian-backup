# ✅为什么Tomcat可以把线程数设置为200，而不是N+1？

# 典型回答


在实际应用中，设置线程池的核心线程数需要综合考虑多个因素，包括系统的硬件资源、应用的业务场景、应用线程的执行时间等等。因此，线程池核心线程数的推荐值仅仅是一个基础的参考值。



对于Tomcat而言，默认最大线程数是200，默认最小空闲线程数是10。



我认为，这些值应该是经过Tomcat开发团队反复测试和验证的结果，是适合绝大多数场景的。



我们作为使用者，大致可以猜测一下，Tomcat可以设置为200，可能有以下原因：



1. **Tomcat作为Web服务器，其主要的场景是处理短连接请求**。相较于其他应用服务器，Tomcat的请求处理时间相对较短，因此每条请求都不会占用时间太长。
2. **Tomcat作为Web服务器**，与一般的应用程序不同，它需要处理大量的并发请求。因此，t默认线程数设置的大一些，可以满足大多数Web应用的需求。
3. 在Tomcat的默认线程池中，使用了多个优化策略，如可回收线程、无锁化算法等，这些策略可以有效地减少线程创建和销毁的开销，提高线程池的吞吐量和性能。



Tomcat的设计目标是高吞吐量和低延迟，不遵守线程池核心线程数推荐公式，是因为其默认线程池的设置已经经过充分的优化和测试，能够满足大多数的应用场景。



**其实在实际工作中，我们也建议大家不要完全按照公式配置，而是根据你的实际业务情况进行充分压测之后，进行合理的配置。**



> 更新: 2024-07-08 12:11:52  
> 原文: <https://www.yuque.com/hollis666/dr9x5m/lhgig4mvgknhqnqw>