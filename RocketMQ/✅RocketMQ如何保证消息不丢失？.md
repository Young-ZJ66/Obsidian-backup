# ✅RocketMQ如何保证消息不丢失？

# 典型回答


**RocketMQ的消息想要确保不丢失，需要生产者、消费者以及Broker的共同努力，缺一不可。**



首先**在生产者端，消息的发送分为同步和异步两种**，在同步发送消息的情况下，消息的发送会同步阻塞等待Broker返回结果，在Broker确认收到消息之后，生产者才会拿到SendResult。如果这个过程中发生异常，那么就说明消息发送可能失败了，就需要生产者进行重新发送消息。



但是Broker其实并不会立即把消息存储到磁盘上，而是先存储到内存中，内存存储成功之后，就返回给确认结果给生产者了。然后再通过异步刷盘的方式将内存中的数据存储到磁盘上。但是这个过程中，如果机器挂了，那么就可能会导致数据丢失。



如果**想要保证消息不丢失，可以将消息保存机制修改为同步刷盘**，这样，Broker会在同步请求中把数据保存在磁盘上，确保保存成功后再返回确认结果给生产者。



```plain
## 默认情况为 ASYNC_FLUSH 
flushDiskType = SYNC_FLUSH 
```



除了同步发送消息，还有异步发送，**异步发送的话就需要生产者重写SendCallback的onSuccess和onException方法，用于给Broker进行回调。在方法中实现消息的确认或者重新发送。**



**为了保证消息不丢失，RocketMQ肯定要通过集群方式进行部署，Broker 通常采用一主多从部署方式，并且采用主从同步的方式做数据复制。**



当主Broker宕机时，从Broker会接管主Broker的工作，保证消息不丢失。同时，RocketMQ的Broker还可以配置多个实例，消息会在多个Broker之间进行冗余备份，从而保证数据的可靠性。



默认方式下，Broker在接收消息后，写入 master 成功，就可以返回确认响应给生产者了，接着消息将会异步复制到 slave 节点。但是如果这个过程中，Master的磁盘损坏了。那就会导致数据丢失了。



如果**想要解决这个问题，可以配置同步复制的方式，即Master在将数据同步到Slave节点后，再返回给生产者确认结果。**<font style="color:rgb(85, 85, 85);">  
</font>

```plain
## 默认为 ASYNC_MASTER
brokerRole=SYNC_MASTER
```



在消费者端，需要确保在消息拉取并消费成功之后再给Broker返回ACK，就可以保证消息不丢失了，如果这个过程中Broker一直没收到ACK，那么就可以重试。



所以，**在消费者的代码中，一定要在业务逻辑的最后一步**`**return ConsumeConcurrentlyStatus.CONSUME_SUCCESS;**`** **当然，也可以先把数据保存在数据库中，就返回，然后自己再慢慢处理。



但是，需要注意的是RocketMQ和Kafka一样，只能最大限度的保证消息不丢失，但是没办法做到100%保证不丢失。原理类似：



[✅为什么Kafka没办法100%保证消息不丢失？](https://www.yuque.com/hollis666/dr9x5m/vwy7vz63qax9c7ab)



> 更新: 2024-07-08 12:10:39  
> 原文: <https://www.yuque.com/hollis666/dr9x5m/txw2gxr6utxggu60>