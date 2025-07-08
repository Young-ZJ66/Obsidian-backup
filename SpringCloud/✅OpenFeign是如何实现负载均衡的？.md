# ✅OpenFeign 是如何实现负载均衡的？

**OpenFeign自己是没有负载均衡的能力的，他的负载均衡是通过与 Spring Cloud LoadBalancer 集成的（以前支持Ribbon）。**



**主要流程**：OpenFeign会通过服务名称（如 `hollis-service`）查询服务发现系统（如 Eureka、Consul）中注册的服务实例。Spring Cloud LoadBalancer会选择一个服务实例进行请求，并通过负载均衡策略（如轮询、随机等）来决定哪个实例处理请求。Feign 客户端会通过 Spring Cloud LoadBalancer 获取到的服务实例的地址，向该实例发起 HTTP 请求。



[✅LoadBalancer和Ribbon的区别是什么？为什么用他替代Ribbon？](https://www.yuque.com/hollis666/dr9x5m/akhcxgict7a5kx46)



[✅LoadBalancer支持哪些负载均衡策略？如何修改？](https://www.yuque.com/hollis666/dr9x5m/xntmn5zea7y85r82)



> 更新: 2025-03-23 14:30:15  
> 原文: <https://www.yuque.com/hollis666/dr9x5m/ag5skxvies08z9z6>