# ✅什么是Nacos，主要用来作什么？

# 典型回答


Nacos是一个基于云原生架构的动态服务发现、配置管理和服务治理平台。支持多种编程语言和多种部署方式，并且与Spring Cloud等主流的微服务框架深度集成。



配置管理：可以将应用程序的配置信息存储在Nacos的配置中心，通过Nacos实现动态配置管理和灰度发布，从而实现应用程序的动态调整和部署。



服务发现及注册：可以将服务注册到Nacos注册中心，并通过Nacos实现服务的自动发现和负载均衡，从而实现服务的高可用和弹性伸缩。



服务治理：可以通过Nacos实现服务的健康检查、故障转移、服务限流、熔断降级等治理能力，从而提高服务的可靠性和稳定性。



事件监听和推送：可以通过Nacos实现配置变更、服务注册和注销等事件的监听和推送，从而实现应用程序的自动化部署和管理。



# 扩展知识


## 哪些服务用到了Nacos？


1. Spring Cloud Alibaba：Nacos是Spring Cloud Alibaba的核心组件之一，可以和Spring Cloud集成，实现服务发现、负载均衡、配置管理等功能。



2. Dubbo：Nacos是Dubbo 2.7.x版本的服务注册中心和配置中心，可以通过Nacos实现服务的动态发现和配置管理。



3. Kubernetes：Nacos可以作为Kubernetes的服务注册中心和配置管理平台，可以将Kubernetes中的服务注册到Nacos中，并通过Nacos进行服务发现和负载均衡。



4. Service Mesh：Nacos可以作为Service Mesh的控制面板，实现服务的配置管理、流量控制和熔断降级等功能。



> 更新: 2024-07-08 12:11:13  
> 原文: <https://www.yuque.com/hollis666/dr9x5m/pd9b5g79pi3ocg6l>