# ✅Eureka 在 Spring Boot 3.x 之后被移除了，如何替代？

# 典型回答


Spring Boot 3.x 移除了对 Java EE（Jakarta EE）旧 API（如 `javax` 包）的支持，而 Eureka 仍然依赖 `javax.xml.bind` 等 API，**因此官方不再维护 Eureka，并推荐其他方案。  **

****

Eureka的主要功能是实现服务注册中心，所以其实他的替代产品还挺多的，比如nacos、zk、consul等 。



[✅注册中心如何选型？](https://www.yuque.com/hollis666/dr9x5m/yyyve0k3e7hgxg8g)



### Nacos


[✅什么是Nacos，主要用来作什么？](https://www.yuque.com/hollis666/dr9x5m/pd9b5g79pi3ocg6l)



**Nacos**是阿里巴巴开源的服务注册中心和配置中心。与Zookeeper不同的是，Nacos自带了配置中心功能，并提供了更多的可视化配置管理工具。Nacos的目标是成为一个更全面的云原生服务发现、配置和管理平台。



### **Consul**


**Consul**是HashiCorp开源的服务注册中心和配置中心，提供了服务发现、健康检查、KV存储和多数据中心功能。Consul提供了更丰富的健康检查和路由功能，同时也提供了丰富的API和Web UI。



### Zookeeper


**Zookeeper**是最早流行的开源分布式协调服务框架之一，同时也提供了分布式配置中心的功能。Zookeeper以高可用、一致性和可靠性著称，**但是需要用户自己来开发实现分布式配置的功能。**



对比如下：

| | Nacos	 | Eureka	 | Consul	 | Zookeeper |
| --- | --- | --- | --- | --- |
| CAP | <font style="color:rgb(79, 79, 79);">CP+AP</font> | AP | CP | CP |
| 健康检查 | <font style="color:rgb(79, 79, 79);">TCP/HTTP/MYSQL/Client Beat</font> | <font style="color:rgb(79, 79, 79);">Client Beat</font> | <font style="color:rgb(79, 79, 79);">TCP/HTTP/gRPC/Cmd</font> | <font style="color:rgb(79, 79, 79);">Keep Alive</font> |
| 负载均衡 | <font style="color:rgb(79, 79, 79);">权重/   </font><font style="color:rgb(79, 79, 79);">metadata/Selector</font> | <font style="color:rgb(79, 79, 79);">Ribbon</font> | <font style="color:rgb(79, 79, 79);">Fabio</font> | <font style="color:rgb(79, 79, 79);">—</font> |
| 一致性算法 | Raft/Distro | Gossip | <font style="color:rgb(55, 65, 81);background-color:rgb(247, 247, 248);">Raft</font> | ZAB |
| 雪崩保护 | <font style="color:rgb(79, 79, 79);">有</font> | <font style="color:rgb(79, 79, 79);">有</font> | <font style="color:rgb(79, 79, 79);">无</font> | <font style="color:rgb(79, 79, 79);">无</font> |
| 访问协议 | <font style="color:rgb(79, 79, 79);">HTTP/DNS</font> | <font style="color:rgb(79, 79, 79);">HTTP</font> | <font style="color:rgb(79, 79, 79);">HTTP/DNS</font> | <font style="color:rgb(79, 79, 79);">TCP</font> |
| 跨注册中心同步 | <font style="color:rgb(79, 79, 79);">支持</font> | <font style="color:rgb(79, 79, 79);">不支持</font> | <font style="color:rgb(79, 79, 79);">支持</font> | <font style="color:rgb(79, 79, 79);">不支持</font> |
| Spring Cloud集成 | <font style="color:rgb(79, 79, 79);">支持</font> | <font style="color:rgb(79, 79, 79);">支持</font> | <font style="color:rgb(79, 79, 79);">支持</font> | <font style="color:rgb(79, 79, 79);">支持</font> |
| Dubbo集成 | <font style="color:rgb(79, 79, 79);">支持</font> | <font style="color:rgb(79, 79, 79);">不支持</font> | <font style="color:rgb(79, 79, 79);">支持</font> | <font style="color:rgb(79, 79, 79);">支持</font> |
| K8s集成 | <font style="color:rgb(79, 79, 79);">支持</font> | <font style="color:rgb(79, 79, 79);">不支持</font> | <font style="color:rgb(79, 79, 79);">支持</font> | <font style="color:rgb(79, 79, 79);">支持</font> |




> 更新: 2025-03-23 13:42:26  
> 原文: <https://www.yuque.com/hollis666/dr9x5m/fgsge63ygay8ml4z>