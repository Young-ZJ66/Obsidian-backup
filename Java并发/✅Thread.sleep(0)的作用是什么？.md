# ✅Thread.sleep(0)的作用是什么？

# 典型回答


Thread的sleep会让线程暂时释放CPU资源，然后进入到TIMED_WAITING状态，等到指定时间之后会再尝试获取CPU时间片。



sleep方法需要指定一个时间，表示sleep的毫秒数，但是有的时候我们会见到Thread.sleep(0)



**这种用法其实就是让当前线程释放一下CPU时间片，然后重新开始争抢。**



这种用法一般比较少见，很多时候在一些底层框架中，可以用来做线程调度，比如某个线程长时间占用CPU资源，这时候通过sleep(0)让线程主动释放CPU时间片，让其他线程可以进行一次公平的争抢。



> 更新: 2024-07-08 12:11:30  
> 原文: <https://www.yuque.com/hollis666/dr9x5m/dazanh67q9re25lp>