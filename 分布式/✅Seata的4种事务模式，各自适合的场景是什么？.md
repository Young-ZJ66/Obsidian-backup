# ✅Seata的4种事务模式，各自适合的场景是什么？

[✅Seata的实现原理是什么](https://www.yuque.com/hollis666/dr9x5m/qro9fl9lsiinx1tu)



+ AT模式
+ TCC模式
+ Saga模式
+ XA模式





首先<font style="color:#DF2A3F;">AT模式</font>，它的**优点**就是没有侵入性，你只需要按照Seata的要求引入@GlobalTransaction注解，就可以实现你的分布式事务了，他不需要做额外的操作，你只需要关注你的业务逻辑即可。



[✅Seata的AT模式的实现原理](https://www.yuque.com/hollis666/dr9x5m/me3ge4vavi0fokgq)



但是他的**局限性**就是只能支持那种具有ACID属性的关系型数据库的操作，比如MySQL，因为他要基于日志进行回滚。如果你的项目中，需要把写数据库和写Redis放到同一个分布式事务中，AT模式就不支持了。



其次是<font style="color:#DF2A3F;">TCC模式</font>，这种模式可以支持多数据源的情况，不管你是Redis、MySQL还是ES，反正他就是要你自己实现Try、Confirm和Cancel，具体的逻辑你自己写，提交、回滚的代码你自己来实现就行了，所以他对代码有一定的侵入性。



[✅什么是TCC，和2PC有什么区别？](https://www.yuque.com/hollis666/dr9x5m/xhvbak3ouy6xqiml)



还有就是<font style="color:#DF2A3F;">Saga这种模式</font>，它适合长事务，什么是长事务呢？就是那种你有外部交互的场景，比如你要调微信支付，就可以用这种模式来管理这个分布式事务。



以上三种都是最终一致性，而<font style="color:#DF2A3F;">XA模式</font>这种就适合于你对一致性要求非常高的场景，只有他是一种强一致性模型。



[✅Seata的AT模式和XA有什么区别？](https://www.yuque.com/hollis666/dr9x5m/fzd9nmraf5krr4m0)



| | XA | AT | TCC | Saga |
| --- | --- | --- | --- | --- |
| 一致性 | 强一致 | 弱一致 | 弱一致 | 最终一致 |
| 隔离性 | 完全隔离 | 基于全局锁隔离 | 基于资源预留隔离 | 无隔离 |
| 代码侵入性 | 无 | 无 | 有，要编写TCC三个接口 | 有，要编写状态机及补偿代码 |
| 性能 | 差 | 高 | 非常高 | 非常高 |
| 适用场景 | 对一致性、隔离性要求较高的场景 | 基于关系型数据库的大多数分布式事务场景 | 对性能要求高的场景，有非关系型数据库要参与的事务 | 业务流程长且多。<br/>参与者包含外部接口或者遗留接口，无法做TCC模式的 |




> 更新: 2024-07-08 12:11:26  
> 原文: <https://www.yuque.com/hollis666/dr9x5m/cx86tg6tdhmz1dm9>