# ✅run/start、wait/sleep、notify/notifyAll区别?

## run方法和start方法区别


我们创建好线程之后，想要启动这个线程，则需要调用其start方法。所以，**start方法是启动一个线程的入口。**



如果在创建好线程之后，直接调用其run方法，那么就会在单线程中直接运行run方法，不会起到多线程的效果。



## sleep和wait区别


sleep()方法可以在任何地方使用；而**wait()方法则只能在同步方法或同步块中使用**。



**wait 方法会释放对象锁**，但 sleep 方法不会。



**wait的线程会进入到WAITING状态，直到被唤醒**；sleep的线程会进入到TIMED_WAITING状态，等到指定时间之后会再尝试获取CPU时间片。



因为Java锁的目标是对象，而wait需要释放锁，所以针对的目标都是对象，所以把他定义在Object类中。 而sleep()不需要释放锁，所以他针对的目标是线程，所以定义在Thread类中。 

## notify和notifyAll区别


当一个线程进入wait之后，就必须等其他线程notify()/notifyAll()，才会从等待队列中被移出。



**使用notifyAll，可以唤醒所有处于wait状态的线程，使其重新进入锁的争夺队列中，而notify只能唤醒一个。**



但是唤醒的这些线程只是进入争夺队列，并不表示立即就可以获得CPU开始执行，因为wait方法被调用的时候，线程已经释放了对象锁。



所以，被notify()/notifyAll()唤醒的线程，只是表示他们可以竞争锁了，竞争到锁之后才有机会被CPU调度。



那么notifyAll虽然可以把所有线程都唤醒，让他们都可以竞争锁，但是最终也只有一个可以获得锁并执行。



**notify和notifyAll因为也是操作对象的，所以把他们定义在Object类中。**



> 更新: 2024-07-08 12:11:13  
> 原文: <https://www.yuque.com/hollis666/dr9x5m/bw9p42>