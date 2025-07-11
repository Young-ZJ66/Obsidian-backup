# ✅有什么情况会导致一个bean无法被初始化么？

# 典型回答


如果一个Bean是正常的Bean，没有缺少必要的注解，也确实在Spring的上下文中的话，无法被初始化，可能考虑的因素是循环依赖的情况。



我们知道，Spring其实是解决了循环依赖的，使用的方案是三级缓存，但是并不是所有的情况他都解决了。



[✅三级缓存是如何解决循环依赖的问题的？](https://www.yuque.com/hollis666/dr9x5m/ffk7dlcrwk35glpl)



但是，**需要注意的是，在SpringBoot 2.6以前，是默认支持三级缓存解决循环依赖的，但是在 SpringBoot 2.6 开始，默认已经不开启对循环依赖的支持了！！！**



[✅Spring默认支持循环依赖吗？如果发生如何解决？](https://www.yuque.com/hollis666/dr9x5m/dzzz1gn5k0rdadvu)



所有，当出现一个Bean无法被初始化的时候，要考虑下是不是这个原因导致的，具体的解决方案在上面的文章中介绍了，在配置文件中加入`spring.main.allow-circular-references=true`或者用`@Lazy` 注解，在`@Autowired` 地方增加即可。



那么，除了以上这种情况外，**如果遇到了非单例的bean，或者是构造器注入也是不行的。**



[✅什么是Spring的循环依赖问题？](https://www.yuque.com/hollis666/dr9x5m/xgbtp0#m0U0D)



构造器注入的循环依赖，可以通过以下的手段解决：



**1、重新设计，彻底消除循环依赖**



循环依赖，一般都是设计不合理导致的，可以从根本上做一些重构，来彻底解决，



**2、改成非构造器注入**



可以改成setter注入或者字段注入。



**3、使用@Lazy解决**



> 更新: 2025-05-04 16:05:19  
> 原文: <https://www.yuque.com/hollis666/dr9x5m/vga6ntoo2obg59gh>