# ✅分布式系统，用户登录信息保存在服务器A上，服务器B如何获取到共享Session

# 典型回答


场景题场景题，其实拆解一下就是八股文，这个问题归根结底，问你的就是如何实现分布式Session。



[✅怎么实现分布式Session？](https://www.yuque.com/hollis666/dr9x5m/xbgu80vgxnhhb438)



在上面这篇文章中我们介绍了很多分布式 Session的方案，其中**最常用的就是用 Redis 来保存了**。



其实就是把用户的登录信息保存在 Redis 中，然后 A 服务器和 B 服务器都从这个 Redis 中读取 Session。主要的流程如下：



![317df68bef78f125aaa0494a7b6af498.svg](./img/V5a0Qy1uYlUKeWJd/317df68bef78f125aaa0494a7b6af498-884266.svg)



除了用 Redis 以外，还可以用其他的第三方存储，比如MySQL，mongodb，等等的都可以的。



除了用 Redis 以外，还有一些其他方案，在上面的文章中都提到了，就不展开说了，如客户端存储、粘性 Session、Session 复制等等



> 更新: 2024-09-07 14:03:26  
> 原文: <https://www.yuque.com/hollis666/dr9x5m/ggzx17g775wy6fye>