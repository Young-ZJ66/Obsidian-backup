# ✅Dubbo服务发现与路由的概念有什么不同？

# 典型回答


服务发现是指在Dubbo注册中心中查找提供某个服务的服务提供者，以便服务消费者可以调用它们。



Dubbo的注册中心可以是ZooKeeper、Redis等，服务提供者在启动时会将自己的地址信息注册到注册中心中，服务消费者在调用服务时会从注册中心中获取服务提供者的地址信息。



服务路由是指根据一定的规则将服务请求路由到指定的服务提供者上。Dubbo提供了多种路由策略，如随机路由、轮询路由、一致性哈希路由等。路由规则可以在Dubbo的配置文件中进行配置，也可以在运行时通过API进行动态修改。



因此，**服务发现是获取服务提供者的地址信息，路由则是将服务请求路由到指定的服务提供者上**。两者都是Dubbo中非常重要的概念，但是它们的作用是不同的。



> 更新: 2024-07-08 12:10:37  
> 原文: <https://www.yuque.com/hollis666/dr9x5m/fryg5kpce4epa29t>