# ✅Eureka和Zookeeper有什么区别？

# 典型回答


Zookeeper是最早流行的开源分布式协调服务框架之一，同时也提供了分布式配置中心的功能。Zookeeper以高可用、一致性和可靠性著称，但是需要用户自己来开发实现分布式配置的功能。



Eureka是Netflix开源的服务注册中心，被广泛应用在Spring Cloud微服务架构中。它提供了易于使用的REST API和Web界面，并支持基于Region和Zone的服务分组和负载均衡。



**设计哲学**：

+ Zookeeper 的设计哲学是 "CP"，即保证一致性和分区容错性。<font style="color:rgb(13, 13, 13);">使用了 ZAB协议来保证集群中的数据强一致性。</font>因为他是一个分布式协调组件，一致性很重要，
+ Eureka的 设计哲学是 "AP"，即保证可用性和分区容错性。他采用了一种更为宽松的一致性模型，支持最终一致性。因为他就是为了做注册中心的，可用性更重要。



[✅什么是CAP理论，为什么不能同时满足？](https://www.yuque.com/hollis666/dr9x5m/avwops)



**性能：**

+ Eureka: 由于其设计重点放在高可用性和可伸缩性上，对于大规模的服务发现场景，Eureka 可以更快地响应服务注册和发现请求。
+ Zookeeper: 他主要是分布式协调组件，最终保证的是一致性，那势必就会牺牲一部分的性能（可用性）。



**客户端交互：**

+ Eureka: 客户端需要定期向 Eureka 发送心跳来维持注册状态，并从 Eureka 获取服务列表。
+ Zookeeper: 客户端可以设置监听器来监控数据节点的变化，当这些节点发生变化时，Zookeeper 会通知客户端。



以上是主要区别，还有些其他区别如下：

| | Eureka	 | Zookeeper |
| --- | --- | --- |
| CAP | AP | CP |
| 健康检查 | <font style="color:rgb(79, 79, 79);">Client Beat</font> | <font style="color:rgb(79, 79, 79);">Keep Alive</font> |
| 负载均衡 | <font style="color:rgb(79, 79, 79);">Ribbon</font> | <font style="color:rgb(79, 79, 79);">—</font> |
| 一致性算法 | Gossip | ZAB |
| 雪崩保护 | <font style="color:rgb(79, 79, 79);">有</font> | <font style="color:rgb(79, 79, 79);">无</font> |
| 访问协议 | <font style="color:rgb(79, 79, 79);">HTTP</font> | <font style="color:rgb(79, 79, 79);">TCP</font> |
| Spring Cloud集成 | <font style="color:rgb(79, 79, 79);">支持</font> | <font style="color:rgb(79, 79, 79);">支持</font> |
| Dubbo集成 | <font style="color:rgb(79, 79, 79);">不支持</font> | <font style="color:rgb(79, 79, 79);">支持</font> |
| K8s集成 | <font style="color:rgb(79, 79, 79);">不支持</font> | <font style="color:rgb(79, 79, 79);">支持</font> |




说这么多，该怎么选择呢？



建议"专业的事，交给专业的人做"，Eureka是专门做注册中心的，所以他的各种保护机制、一致性保证、监控等都会更加专注一些。



> 更新: 2024-07-08 12:11:50  
> 原文: <https://www.yuque.com/hollis666/dr9x5m/ifgriifpma4mgpu0>