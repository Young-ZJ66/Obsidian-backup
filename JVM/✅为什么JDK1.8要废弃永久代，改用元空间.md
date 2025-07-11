# ✅为什么JDK  1.8要废弃永久代，改用元空间

# 典型回答


我们知道，从JDK 1.8开始，HotSpot虚拟机对方法区的实现进行了重大改变。永久代被移除，取而代之的是**元空间（Metaspace）**

****

先说下他们的区别，然后你大概也就能懂了为啥要这么改了。



**永久代是堆上的一部分，大小收堆大小的限制，容易发生OOM。元空间在本地内存上，不受堆大小的限制，不容易发生OOM。**



因为方法区作为元空间和永久代的主要区域，他里面存储了大量的被加载的类，而很多时候，项目中用了很多动态生成类的框架之后，比如Spring、等等，就会占用很多空间，如果在堆上，就会导致频繁的GC，以及OOM的问题。



而把方法区放到元空间，即放到堆外内存中， JVM 可以根据机器内存大小**动态扩展**元空间的大小，减少OOM的发生。



我还在其他资料上，看到有人提过，说不同 JVM 实现（比如 Oracle JDK、IBM J9）对 PermGen 细节不同，导致移植性很差。而且HotSpot 团队自己也觉得 PermGen 的管理逻辑太混乱，扩展维护困难。（这两点知道即可，不用深究）



> 更新: 2025-04-26 16:53:08  
> 原文: <https://www.yuque.com/hollis666/dr9x5m/oze6rrdt2yeq1o02>