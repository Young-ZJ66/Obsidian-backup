# ✅Netty有哪些序列化协议？

# 典型回答


Netty支持很多种序列化协议，基本上市面上常见的序列化协议他都支持的。如：



Java原生序列化：Java原生的序列化协议，可以序列化所有实现了Serializable接口的对象。Java序列化虽然简单易用，但是序列化后的字节数较大，序列化性能较差，且不具备跨语言的能力，因此不太常用。



JSON序列化：JSON是一种轻量级的数据交换格式，易于阅读和编写，同时也具备跨语言的能力，因此在分布式系统中广泛使用。Netty内置了多种JSON序列化库，包括Jackson、FastJSON等。



XML序列化：XML也是一种常用的数据交换格式，可以用于跨语言的数据交换。Netty内置了多种XML序列化库，包括JAXB、XStream等。



Protobuf序列化：Protobuf是Google开源的一种高效、灵活的二进制序列化协议，具有良好的跨语言能力和高效的序列化性能，被广泛应用于分布式系统中。Netty内置了对Protobuf的支持。



Thrift序列化：Thrift也是一种由Apache开源的二进制序列化协议，具有跨语言、高效等特点，被广泛应用于分布式系统中。Netty也提供了对Thrift的支持。



> 更新: 2024-07-08 12:11:51  
> 原文: <https://www.yuque.com/hollis666/dr9x5m/feghdunr7kut0y9k>