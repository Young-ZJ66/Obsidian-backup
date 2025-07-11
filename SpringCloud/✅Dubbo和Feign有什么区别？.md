# ✅Dubbo和Feign有什么区别？

# 典型回答


Dubbo 和 Feign 都是常用于构建分布式系统的技术，主要解决的问题就是多个微服务之间的相互调用。他们之间有一些区别，主要体现在它们所服务的架构、通信协议、性能特点以及集成与使用方式上。



**Dubbo 是一个高性能的、基于 Java 的开源RPC（远程过程调用）框架。它主要用于构建高性能和透明化的服务间远程调用的微服务架构。Dubbo 支持多种通信协议和负载均衡策略，允许服务之间以高效率进行数据交换。**



Dubbo的主要特点：

+ **高性能的RPC调用**：提供基于接口的远程方法调用。
+ **多种通信协议支持**：支持多种协议如 Dubbo、HTTP、RMI 等。
+ **服务治理**：内建的服务治理功能，包括服务发现、负载均衡、故障转移和动态配置等。
+ **依赖Zookeeper、Nacos等注册中心**：用于服务的注册与发现。



****

**Feign 是一个声明式的Web服务客户端，它使得编写Web服务客户端变得更容易。使用 Feign 可以通过简单的接口和注解来调用HTTP API。Feign 的目标是尽可能简化HTTP API客户端的实现过程。**



Feign主要特点：

+ **声明式的HTTP客户端**：通过Java接口和注解来定义方法与远程服务的绑定关系。
+ **集成Ribbon和Hystrix**：支持负载均衡（通过集成Ribbon）和服务熔断（通过集成Hystrix）。
+ **主要用于Spring Cloud**：通常与Spring Cloud组件一起使用，实现服务间的调用。





**主要区别：**

| | **Dubbo** | **Feign** |
| --- | --- | --- |
| **设计哲学** | RPC | HTTP |
| **通信协议** | 支持多种协议，如Dubbo、HTTP等 | HTTP |
| **服务治理** | 支持 | 支持较少 |
| **调用性能** | 强 | 没那么强 |
| **负载均衡** | 内置 | 依赖Ribbon提供 |
| **注册中心** | 依赖Nacos、Zookeeper等 | 依赖Nacos、Eureka等 |
| **服务发现** | 内置 | 依赖Nacos、Eureka等 |
| **生态** | SpringCloudAlibaba | SpringCloud |
| **停止更新** | 未停止 | 已停止 |




<u>总结来说，Dubbo 和 Feign 虽然都用于服务间的调用，但Dubbo 更注重于RPC的高性能实现和服务治理，而Feign 更侧重于简化HTTP服务的消费和集成Spring Cloud生态。选择哪个工具取决于你的具体需求、架构风格和技术栈。</u>



> 更新: 2024-07-13 16:39:25  
> 原文: <https://www.yuque.com/hollis666/dr9x5m/bi8engr1dqg1o4gn>