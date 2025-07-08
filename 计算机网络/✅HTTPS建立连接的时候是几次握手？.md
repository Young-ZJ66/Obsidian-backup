# ✅HTTPS建立连接的时候是几次握手？

# 典型回答


这里其实考察的是TCP的三次握手，以及HTTPS相比HTTP中需要增加的TLS/SSL，但是其实TLS的数据交换并不叫握手，没有这么叫的，他只是数据交换而已。



**需要TCP的3次握手，在根据TLS的版本，做2-4步的加密通道建立（TLS 1.2需要4步，TLS 1.3需要2步）。**



首先是需要进行TCP的三次握手，用来建议TCP的连接

+ 第一次握手：客户端发送`SYN`包（同步序列编号）到服务器，进入`SYN_SENT`状态。
+ 第二次握手：服务器返回`SYN-ACK`包（确认客户端的SYN），进入`SYN_RCVD`状态。
+ 第三次握手：客户端发送`ACK`包确认服务器的SYN，完成TCP连接建立。



[✅什么是TCP三次握手、四次挥手？](https://www.yuque.com/hollis666/dr9x5m/gbsihwp8q22wc3cn)



接下来通过TLS来建立加密通道，根据不同的版本看，情况不一样。以TLS 1.2为例（需2个往返，共4步）：

+ ClientHello：发送客户端支持的TLS版本、加密算法、随机数。
+ ServerHello：服务器选定TLS版本、加密算法、随机数；发送证书（身份验证）、`ServerKeyExchange`（密钥参数，如ECDHE）。
+ 客户端验证证书：生成预主密钥，用服务器公钥加密后发送；计算会话密钥。
+ Finish：双方发送加密的`Finished`消息验证握手完整性。



对于TLS 1.3来说，做了优化（1个往返，共2步）：

+ ClientHello：包含支持的加密算法和密钥共享（Key Share）。
+ ServerHello：选择参数、发送证书、生成会话密钥并直接响应。

<font style="color:rgb(64, 64, 64);"></font>

![1745654892160-fc641a5c-72cd-42dc-865e-1f31e6bc7f51.webp](./img/iwKrFhQzUsrmJy0F/1745654892160-fc641a5c-72cd-42dc-865e-1f31e6bc7f51-841434.webp)

（图片来自网络）



> 更新: 2025-04-26 16:14:41  
> 原文: <https://www.yuque.com/hollis666/dr9x5m/mkzzeex754d5w2fq>