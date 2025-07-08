# ✅为什么logger.warn()之前要使用logger.isWarnEnabled()？

# 典型回答


很多人在读源码的时候，经常可以看到以下代码：



Spring中：

![1699169900674-ea85e8aa-ae76-4fda-b516-ff6350b1be64.png](./img/DvdkuXzFiTagUt99/1699169900674-ea85e8aa-ae76-4fda-b516-ff6350b1be64-072726.png)



Dubbo中：

![1699169943116-7eb05894-f704-4b33-ac40-f5973844595a.png](./img/DvdkuXzFiTagUt99/1699169943116-7eb05894-f704-4b33-ac40-f5973844595a-755169.png)



也就是说，很多框架，在执行warn()、debug()等方法前，都会额外的调用一下isWarnEnabled()和isDebugEnabled()等方法，这是为什么呢？



isWarnEnabled、isDebugEnabled等方法，其实是判断当前日志级别是否开启的，如果开启则返回true，否则返回false。



其实，之所以要提前调用一次isWarnEnabled，主要是为了提升性能的，因为在记录日志时，生成日志消息的过程可能会涉及方法的执行、字符串的拼接、对象的序列化等操作。而这些操作都是比较耗费时间的。



如果一段日志，不需要输出，那么这些步骤其实是可以省略的。



比如我们有以下日志要输出：



```java
public void login(LoginRequest loginRequest){
    if (logger.isWarnEnabled()) {
        logger.warn("This is a message with: " + JSON.toJSONString(loginRequest));
    }
}
```



通过`logger.isWarnEnabled`做一次前置判断，那么就可以在warn级别不生效时，能避免 `JSON.toJSONString(loginRequest)`方法的执行，也能避免`"This is a message with: " + JSON.toJSONString(loginRequest)`这个字符串拼接操作的执行。



所以，使用`logger.isXxxEnabled()`用于检查日志Xxx级别是否启用，可以在需要时避免不必要的开销，提高应用程序的性能。这种做法特别在记录频繁的日志消息时，尤为重要。



> 更新: 2024-07-08 12:11:18  
> 原文: <https://www.yuque.com/hollis666/dr9x5m/zyfbnhr93gd3snz1>