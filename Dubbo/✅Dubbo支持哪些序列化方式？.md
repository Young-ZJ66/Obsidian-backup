# ✅Dubbo支持哪些序列化方式？

# 典型回答


Dubbo是RPC框架，需要远程调用，那么就需要把请求和响应做序列化和反序列化。Dubbo目前支持多种序列化协议。



在[Dubbo 3.0](https://github.com/apache/dubbo/tree/3.3/dubbo-serialization) 中，内置了3种序列化协议：

![1704532702023-a1278f43-e27b-454b-be83-e59cadb48006.png](./img/caLP1fWeG7uIC49K/1704532702023-a1278f43-e27b-454b-be83-e59cadb48006-388507.png)



比较常见的有：



1. **<font style="color:rgb(34, 34, 34);">Hessian2</font>**<font style="color:rgb(55, 65, 81);">：</font>hessian是一种跨语言的高效二进制序列化方式。但这里实际不是原生的hessian2序列化，而是阿里修改过的hessian lite，它是dubbo RPC默认启用的序列化方式
2. **Java**<font style="color:rgb(55, 65, 81);">：标准的Java序列化协议，易于使用但性能相对较低。</font>
3. **fastjson2**<font style="color:rgb(55, 65, 81);">：轻量级的数据交换格式，适用于简单的数据结构，易于阅读和调试。</font>

<font style="color:rgb(55, 65, 81);"></font>

这里面，hessian2是默认的，主要是因为他的性能是最好的，并且它支持跨语言。



而这几年，各种序列化框架层出不穷，今天出了一个号称速度快，明天出一个号称跨语言。总之有很多，于是在[Dubbo的扩展](https://github.com/apache/dubbo-spi-extensions)中，就增加支持很多其他的序列化协议：

<font style="color:rgb(55, 65, 81);"></font>

![1704532830505-c3cefb9f-1ece-484b-b2b1-946738da21ad.png](./img/caLP1fWeG7uIC49K/1704532830505-c3cefb9f-1ece-484b-b2b1-946738da21ad-173952.png)

<font style="color:rgb(55, 65, 81);"></font>

<font style="color:rgb(55, 65, 81);"></font>

其中包括了avro、fastjson、fst、fury、gson、Jackson、kryo、msgpack、protobuf和protostuff等。



这里面很多框架其实性能都比较好，大有代替Hession的势头，比如Kryo、FST、fury等。



比如蚂蚁出的fury框架，号称比hessian快100倍，以下是他的一个整体介绍。详见：[https://developer.aliyun.com/article/992485](https://developer.aliyun.com/article/992485)



![1704533239946-e7a0107a-4e48-42cb-8e3c-54a46795a371.png](./img/caLP1fWeG7uIC49K/1704533239946-e7a0107a-4e48-42cb-8e3c-54a46795a371-850546.png)



> 更新: 2024-07-08 12:10:37  
> 原文: <https://www.yuque.com/hollis666/dr9x5m/xgwzlb4bp9dhg3r0>