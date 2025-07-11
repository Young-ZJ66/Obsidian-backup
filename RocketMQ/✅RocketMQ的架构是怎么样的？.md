# ✅RocketMQ的架构是怎么样的？

# 典型回答


RocketMQ主要由Producer、Broker和Consumer三部分组成，如下图所示：



![1679211487811-e336d552-e96e-49f4-a1ce-121163febc86.png](./img/bobd3VN1F0uLqn9y/1679211487811-e336d552-e96e-49f4-a1ce-121163febc86-418536.png)



1. Producer：消息生产者，负责将消息发送到Broker。
2. Broker：消息中转服务器，负责存储和转发消息。RocketMQ支持多个Broker构成集群，每个Broker都拥有独立的存储空间和消息队列。
3. Consumer：消息消费者，负责从Broker消费消息。
4. NameServer：名称服务，负责维护Broker的元数据信息，包括Broker地址、Topic和Queue等信息。Producer和Consumer在启动时需要连接到NameServer获取Broker的地址信息。
5. Topic：消息主题，是消息的逻辑分类单位。Producer将消息发送到特定的Topic中，Consumer从指定的Topic中消费消息。
6. Message Queue：消息队列，是Topic的物理实现。一个Topic可以有多个Queue，每个Queue都是独立的存储单元。Producer发送的消息会被存储到对应的Queue中，Consumer从指定的Queue中消费消息。



> 更新: 2024-07-08 12:10:39  
> 原文: <https://www.yuque.com/hollis666/dr9x5m/fkx1hga7xlpbfbuv>