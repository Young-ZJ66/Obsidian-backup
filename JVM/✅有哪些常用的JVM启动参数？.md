# ✅有哪些常用的JVM启动参数？

# 典型回答


JVM的启动参数有很多，但是我们平常能用上的并不是特别多，这里介绍几个我们常用的：



1. **堆设置**：
    - -Xms：设置堆的初始大小。
    - -Xmx：设置堆的最大大小。
2. **栈设置**：
    - -Xss：设置每个线程的栈大小。
3. **垃圾回收器设置**：
    - -XX:+UseG1GC：使用 G1 垃圾回收器。
    - -XX:+UseParallelGC：使用并行垃圾回收器。
4. **性能调优**：
    - -XX:PermSize 和 -XX:MaxPermSize：在 Java 8 之前设置永久代的初始大小和最大大小。
    - -XX:MetaspaceSize 和 -XX:MaxMetaspaceSize：在 Java 8 及以上版本设置 Metaspace 的初始大小和最大大小。
    - -XX:+PrintGCDetails：打印垃圾回收的详细信息。
5. **调试和分析**：
    - -verbose:gc：输出垃圾回收的详细信息。
    - -XX:+HeapDumpOnOutOfMemoryError：在内存溢出时生成堆转储。



# 扩展知识


## 如何使用


要使用这些 JVM 启动参数，你需要在启动 Java 应用程序时在命令行中指定它们。



例如，如果你想设置最大堆大小为 512MB 并启用 G1 垃圾回收器，你可以这样启动你的 Java 应用程序：



```java
java -Xmx512m -XX:+UseG1GC -jar your-application.jar
```





另外，如果是在IDEA中，需要再run配置中增加上对应的参数，如：



![1704001546418-690df6e2-978d-47c8-8be3-190e26272bb0.png](./img/hQBy_FQWBIfPcfuC/1704001546418-690df6e2-978d-47c8-8be3-190e26272bb0-015302.png)

（图片来源于网络）



> 更新: 2024-07-08 12:11:20  
> 原文: <https://www.yuque.com/hollis666/dr9x5m/nw8et6>