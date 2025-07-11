# ✅用@Scheduled执行定时任务，如何避免集群的并发问题

# 典型回答


在 Spring Boot 项目中，`@Scheduled` 默认在每个实例上都会执行一次任务。如果你的应用部署在**集群环境**下，所有节点都会执行 `@Scheduled` 任务，可能导致**并发问题。**



那么如何解决呢？



他山之石，可以攻玉，先看看xxl-job是咋解决的：



[✅xxl-job如何保证一任务只会触发一次？](https://www.yuque.com/hollis666/dr9x5m/kgrtbyygyu5wnsgx)



他是基于数据库的悲观锁，多个实例执行的时候，大家一起抢锁，谁抢到了谁执行。



所以，我们也可以用**<u>悲观锁</u>**的思想。



不管使用xxl-job这种select for update的悲观锁，还是基于Redis、Zookeeper来实现分布式锁，都是同样的思想，就是谁抢到锁，谁执行。



几种分布式锁实现方式如下：



[✅分布式锁有几种实现方式？](https://www.yuque.com/hollis666/dr9x5m/fvnr41)



但是需要注意，这里最好用非阻塞锁，抢锁失败就直接返回失败，而不是要一直等。那么就可以用redis的tryLock代替lock。



除了加锁之外，还可以用另外一种方案，那就是**<u>选主</u>**

****

大家不妨想一下，其实是加分布式锁，谁抢到谁执行，这其实就是一种选主，大家一起选择一个master，谁是master谁执行。



那么，就可以用zookeeper，它能实现master选举的能力，任务执行的时候去选主，如果选举成功，则给他执行，否则就不执行。



除了以上方案外，再追问的话，就只能废弃到Scheduling Task这种用法了，用XXL-JOB、 Quartz  等框架代替。



> 更新: 2025-03-15 15:07:33  
> 原文: <https://www.yuque.com/hollis666/dr9x5m/gy31zq2gdufg3tfx>