# ✅什么是分布式BASE理论？

# 典型回答


BASE理论是对CAP理论的延伸，核心思想是即使无法做到强一致性（Strong Consistency，CAP的一致性就是强一致性），但应用可以采用适合的方式达到最终一致性（Eventual Consitency）。



BASE是指基本可用（Basically Available）、软状态（ Soft State）、最终一致性（ Eventual Consistency）。



做不到100%可用，那么就做到基本可用。做不到强一致性，那么就做到最终一致性。



**想要做到BASE，那么主要就是用这几个手段：中间状态（软状态）+重试（最终一致性）+降级（基本可用）**

## <font style="color:rgb(85, 85, 85);">基本可用（Basically Available）</font>
基本可用是指分布式系统在出现故障的时候，允许损失部分可用性（降级），即保证核心可用。



电商大促时，为了应对访问量激增，部分用户可能会被引导到降级页面，服务层也可能只提供降级服务。这就是损失部分可用性的体现。



[✅什么是服务降级？](https://www.yuque.com/hollis666/dr9x5m/eukvb5)



## <font style="color:rgb(85, 85, 85);">软状态（ Soft State）</font>
软状态是指允许系统存在中间状态，而该中间状态不会影响系统整体可用性。分布式存储中一般一份数据至少会有三个副本，允许不同节点间副本同步的延时就是软状态的体现。mysql replication的异步复制也是一种体现。



其实就是中间状态，比如当前INIT，然后处理中推进到PROCESSING，然后可以基于这个PROCESSING不断重试，直到推进到SUCCESS



有了软状态，我们才能重试。

## <font style="color:rgb(85, 85, 85);">最终一致性（ Eventual Consistency）</font>
最终一致性是指系统中的所有数据副本经过一定时间后，最终能够达到一致的状态。弱一致性和强一致性相反，最终一致性是弱一致性的一种特殊情况。

# 扩展知识
## ACID和BASE的区别与联系


ACID是传统数据库常用的设计理念，追求强一致性模型。BASE支持的是大型分布式系统，提出通过牺牲强一致性获得高可用性。



ACID和BASE代表了两种截然相反的设计哲学



在分布式系统设计的场景中，系统组件对一致性要求是不同的，因此ACID和BASE又会结合使用。



> 更新: 2024-07-08 12:12:06  
> 原文: <https://www.yuque.com/hollis666/dr9x5m/vfnqpd>