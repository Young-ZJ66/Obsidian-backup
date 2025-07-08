# ✅最强应届生，JVM，计算机网络

# 面试者背景


:::warning
今日面试者：双非24届，准备春招，缓存组件项目，抖音短视频项目。

挑一个最复杂的模块介绍下流程。发视频&获得视频列表。MinIO，如何实现刷过的视频不会再刷到。

如果视频特别大，会做压缩吗？这两个模块你觉得哪里还能优化？

敏感词过滤怎么实现的？除了前缀树还有其他的吗？DFA算法知道吗？

登录密码增强怎么做的？MD5是加密算法吗？为啥可以防止彩虹表攻击？随机加盐、多次hash、

对称加密和非对称加密区别是啥？

视频的唯一的URL地址生成方式？雪花算法。为啥不用uuid？雪花算法用的哪个工具类？

进程和线程、协程有啥区别？Java是多进程还是多线程，Java的线程是如何实现的知道吗。什么语言支持协程？go、java

进程间通信方式有哪些？管道（半双工和全双工区别）、CPU和GPU有啥区别？为啥大模型训练用GPU。TCP为啥需要三次握手？TCP对头阻塞是啥？能解决吗？ping的原理是什么？ping localhost没网吗？ping需要端口吗？

CMS的垃圾回收过程。为啥要分成4步。为啥初始标记和重新标记需要STW？什么东西可以当做GC Root。跨代引用怎么办？fullgc和younggc都会吗？

安全点了解吗？如果有一段代码进不了安全点怎么办？什么是安全区域？除了GC还有其他场景用安全点吗？锁降级、Dump、jit、热替换

Java的类加载机制。双亲委派模型。有哪些类加载器？bootstrap、ext、app，哪个版本是这样的？后面有变化吗？

JDK 8以后的版本有哪些新特性？模块化知道吗？ZGC了解吗？G1知道吗，和CMS区别？位置、算法、AOT编译知道吗？

设计模式用过吗？多个支付渠道的实现，用什么设计模式实现？策略+模板+工厂

频繁FullGC排查如何做？dump、MAT。如何获取dump？dump之前发生了GC怎么办？不做dump能定位fullgc原因吗？

:::

# 题目解析


:::color4
登录密码增强怎么做的？MD5是加密算法吗？为啥可以防止彩虹表攻击？随机加盐、多次hash、

对称加密和非对称加密区别是啥？

:::



[✅MD5是加密算法吗？绝对安全吗？](https://www.yuque.com/hollis666/dr9x5m/nmo3mutxsll6ch8s)



[✅对称加密和非对称加密有什么区别？](https://www.yuque.com/hollis666/dr9x5m/reb5c7)



[✅什么是对称加密和非对称加密？](https://www.yuque.com/hollis666/dr9x5m/oq72da9rrpyt34g8)

:::color4
视频的唯一的URL地址生成方式？雪花算法。为啥不用uuid？雪花算法用的哪个工具类？

:::



[✅什么是UUID，能保证唯一吗？](https://www.yuque.com/hollis666/dr9x5m/pi2zfc9ykug141im)



[✅什么是雪花算法，怎么保证不重复的？](https://www.yuque.com/hollis666/dr9x5m/rsocc4sd7v9i0pvc)





:::color4
进程和线程、协程有啥区别？Java是多进程还是多线程，Java的线程是如何实现的知道吗。什么语言支持协程？go、java

进程间通信方式有哪些？管道（半双工和全双工区别）、CPU和GPU有啥区别？为啥大模型训练用GPU。

:::



[✅进程，线程和协程的区别](https://www.yuque.com/hollis666/dr9x5m/gnieul)



[✅JDK21 中的虚拟线程是怎么回事？](https://www.yuque.com/hollis666/dr9x5m/ac1a0q)



[✅进程间通信方式有哪些？](https://www.yuque.com/hollis666/dr9x5m/yrgn3o0q1t1t0ph8)



[✅什么是全双工和半双工](https://www.yuque.com/hollis666/dr9x5m/mnq17i)



[✅GPU和CPU区别？为什么挖矿、大模型都用GPU？](https://www.yuque.com/hollis666/dr9x5m/dgu1mwxhton2npoi)





:::color4
TCP为啥需要三次握手？TCP对头阻塞是啥？能解决吗？ping的原理是什么？ping localhost没网吗？ping需要端口吗？

:::



[✅什么是TCP三次握手、四次挥手？](https://www.yuque.com/hollis666/dr9x5m/gbsihwp8q22wc3cn)



[✅为什么需要HTTP/2，他解决了什么问题？](https://www.yuque.com/hollis666/dr9x5m/hiqe1d)



[✅ping的原理是什么？](https://www.yuque.com/hollis666/dr9x5m/ivry7a)



:::color4
CMS的垃圾回收过程。为啥要分成4步。为啥初始标记和重新标记需要STW？什么东西可以当做GC Root。跨代引用怎么办？fullgc和younggc都会吗？

:::



[✅介绍下CMS的垃圾回收过程](https://www.yuque.com/hollis666/dr9x5m/lh75qbvh58o6xv8s)



[✅为什么初始标记和重新标记需要STW，而并发标记不需要？](https://www.yuque.com/hollis666/dr9x5m/acz9pk5h7waamrbe)



[✅什么是跨代引用，有什么问题？](https://www.yuque.com/hollis666/dr9x5m/efipfg3pgg4puux2)



:::color4
安全点了解吗？如果有一段代码进不了安全点怎么办？什么是安全区域？除了GC还有其他场景用安全点吗？锁降级、Dump、jit、热替换

:::



[✅什么是safe point，有啥用？](https://www.yuque.com/hollis666/dr9x5m/rpclpg5ag63bkyyq)



:::color4
Java的类加载机制。双亲委派模型。有哪些类加载器？bootstrap、ext、app，哪个版本是这样的？后面有变化吗？

:::



[✅Java中类加载的过程是怎么样的？](https://www.yuque.com/hollis666/dr9x5m/tuikxhaa2urq32ds)



[✅JDK1.8和1.9中类加载器有哪些不同](https://www.yuque.com/hollis666/dr9x5m/mla5wg5f3xwifa1d)





:::color4
JDK 8以后的版本有哪些新特性？模块化知道吗？ZGC了解吗？G1知道吗，和CMS区别？位置、算法、AOT编译知道吗？

:::



[✅JDK新版本中都有哪些新特性？](https://www.yuque.com/hollis666/dr9x5m/htgm9p3vbpx85p6n)



[✅什么是AOT编译？和JIT有啥区别？](https://www.yuque.com/hollis666/dr9x5m/cy5i6guhszisviks)



[✅G1和CMS有什么区别？](https://www.yuque.com/hollis666/dr9x5m/gkhirkk70lc2zz8z)





:::color4
设计模式用过吗？多个支付渠道的实现，用什么设计模式实现？策略+模板+工厂

:::



[✅你在工作中是如何使用设计模式的？](https://www.yuque.com/hollis666/dr9x5m/kzq0dwtbtgps9oe1)





:::color4
频繁FullGC排查如何做？dump、MAT。如何获取dump？dump之前发生了GC怎么办？不做dump能定位fullgc原因吗？

:::



[✅频繁FullGC问题排查](https://www.yuque.com/hollis666/dr9x5m/iocmzc)



[✅频繁FullGC问题排查(2)](https://www.yuque.com/hollis666/dr9x5m/zpkzwgx4o9g89s8x)







> 更新: 2024-07-08 12:11:58  
> 原文: <https://www.yuque.com/hollis666/dr9x5m/zd24lrue0r193c6y>