# ✅什么是QPS，什么是RT？

# 典型回答


QPS，指的是系统每秒能处理的请求数(Query Per Second) ，在Web应用中我们更关注的是Web应用每秒能处理的request数量。这个是衡量系统性能的重要指标。



RT，指的是响应时间(Response Time)，是指从客户端发一个请求开始计时，到客户端接收到从服务器端返回的响应结果结束所经历的时间。





# 扩展知识
## RT


响应时间(Response Time)，是指从客户端发一个请求开始计时，到客户端接收到从服务器端返回的响应结果结束所经历的时间。



当我们评价一个网站的"快"和"慢"的时候，其实说的就是他的RT时间的长和短。当我们访问某个网站，有时候我们会说这个网站很"卡"，其实言下之意说的就是这个网站的RT很长。



如果一个网站的RT很长的话，就会特别的影响用户体验。所以，RT是很重要的一个指标。也是各个网站需要重点优化的。



拿一个游乐园的例子来说明一下可能会比较容易理解，比如我们去迪士尼乐园游玩时候，大多数的项目都是需要排队的。



为了让游客知道一个项目需要排队多久才能玩上，迪士尼做了很多事情，比如他们有一个App，专门可以提示每个项目的预计排队时间。再有就是每个项目的排队处都有一个小牌牌，上面写着预计排队时间。



![1666699215659-da7a747b-61e7-4338-9e90-77ac6c4fab8f.jpeg](./img/yZKSFXdYnaqZYtep/1666699215659-da7a747b-61e7-4338-9e90-77ac6c4fab8f-762695.jpeg)￼



但是，这个时间并不是凭空设定出来的，而是『计算』出来的。



迪士尼的排队时间计算方法：



1、迪士尼在每个项目的入口处和出口处都会设置工作人员。  
2、入口处工作人员随机寻找游客，给游客一张小纸条，上面记录着游客开始排队的时间。  
3、入口处工作人员提醒游客，项目游览玩之后，在出口处把小纸条交还给出口处的工作人员。  
4、出口处工作人员在收到游客的小纸条后，会用：当前时间-游客开始排队的时间 = 排队时长。  
5、为了尽量让数据准确，一般会收集多个排队时长之后，计算一个平均值。



以上就是迪士尼的排队时间计算法。其实，这也是RT的计算方法。在一个请求开始的时候记录时间，请求结束的时候再记录时间，两个时间的差值，就是RT了。



迪士尼的一个项目的RT包含了多个时间段：排队时间、听项目讲解时间、项目准备时间、项目游玩时间等。



服务器响应时间也有多部分组成，一般包含：请求发送时间、网络传输时间和服务器处理时间等三部分。



## QPS 


QPS，指的是系统每秒能处理的请求数(Query Per Second) ，在Web应用中我们更关注的是Web应用每秒能处理的request数量。这个是衡量系统性能的重要指标。有时候，我们也称之为吞吐量。



QPS和RT几乎总是成对出现的。当我们评价迪士尼的一个项目的好坏的时候，通常会包含这几个指标：是否好玩、游玩时长以及可以同时容纳多少人。



这个可以同时容纳多少人，就可以简单的理解为QPS。很大程度上，一个项目同时可以容纳多少人，其实会大大的影响游客的游玩时长。



所以，QPS和RT之间是有着一定的关系的（单线程情况下，多线程的话还要再乘一个线程数）：



```latex
RT= 并发数/QPS
QPS= 并发数/RT
```



虽然上面的等式看上去，在并发数一定的情况下，想要提升QPS的话就只能降低RT。但其实并不是，以上只是QPS的计算方法。想要提升QPS往往有很多手段。



就像想要提升游乐设施的吞吐量，最首先想到的办法就是升级设备，比如增加游乐场地的面积，增加设备的座位数目，增加排队的队伍个数等。



在计算机系统中，想要提升QPS，主要可以在CPU、内存等硬件上面下功夫，比如提升CPU利用率、增加CPU数目、提升内存等。



## 并发用户数
并发用户数指的就是同时跑到一个项目前面排队的人数。  
![1666699215665-3e0a4a3e-958c-48c4-8197-d249ec39f159.jpeg](./img/yZKSFXdYnaqZYtep/1666699215665-3e0a4a3e-958c-48c4-8197-d249ec39f159-771597.jpeg)￼



关于并发用户数有两种常见的错误观点。



一种错误观点是把并发用户数量理解为使用系统的全部用户的数量；（比如迪士尼的飞跃地平线项目一天可能会接纳50万人，我们不能说这个50万就是并发用户数）



还有一种错误观点是把用户在线数量理解为并发用户数量。（比如晚上六点的时候，迪士尼的飞跃地平线项目排队加观看人数共有1万人，我们不能说这个1万就是并发用户数）



并发用户数量的正确理解为：在**同一时刻**与服务器**进行了交互**的**在线用户数量**。（我们说，晚上六点的时候，共有8000人正在排队使用飞跃地平线这个项目。这才是并发用户数）



拿系统来说，我们说淘宝详情页的并发用户数，其实说的是同一时刻请求查看详情页的用户个数。有些用户虽然也在浏览详情页，但是它并没有在并发时刻和系统有交互，这就不算的。



## 最佳线程数


最佳线程数指的就是一个项目最多可以容纳的人数，这里的容纳可以包含排队的人数。  
![1666699215675-ceca63b2-2ac0-43ac-a384-c07234331db3.jpeg](./img/yZKSFXdYnaqZYtep/1666699215675-ceca63b2-2ac0-43ac-a384-c07234331db3-813344.jpeg)￼



迪士尼每新开一个场馆或者一个游戏项目的时候，都会是一个试运营的阶段。在试运营阶段，通过不断调整并发用户数来观察整个场馆或者项目的运行情况。



除了上线新场馆和新项目以外，有的是在节假日之前也会有一些类似的实验。



这和计算机软件的压测很像。就是不断的提高请求数目，来观察系统的QPS和系统的其他指标，如CPU情况、内存情况等。



性能压测的情况下，起初随着用户数的增加，QPS会上升并对CPU等影响不大，当到了一定的阈值之后，用户数量增加QPS并不会增加，或者增加不明显，同时CPU Load有飙高、内存占用大等情况发生。随之而来的伴随着请求的响应时间大幅增加。这个阈值我们认为是最佳线程数。



如果并发请求数目，超过了系统的最佳线程数，那么就会导致激烈的资源竞争，随着资源的匮乏甚至枯竭，整个系统也就面临着灾难。









> 更新: 2024-08-21 23:03:20  
> 原文: <https://www.yuque.com/hollis666/dr9x5m/hr5913>