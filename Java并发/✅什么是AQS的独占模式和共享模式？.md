# ✅什么是AQS的独占模式和共享模式？

# 典型回答


AbstractQueuedSynchronizer（AQS）是Java并发包中的一个核心框架，用于构建锁和其他同步组件。



[✅如何理解AQS？](https://www.yuque.com/hollis666/dr9x5m/qka9yt)



**它提供了一套基于FIFO队列的同步器框架，并支持独占模式和共享模式，这两种模式是用于实现同步组件的关键。**

****

+ 独占模式意味着一次只有一个线程可以获取同步状态。这种模式通常用于实现互斥锁，如ReentrantLock。
+ 共享模式允许多个线程同时获取同步状态。这种模式通常用于实现如信号量（Semaphore）和读写锁（ReadWriteLock的读锁）等同步组件。



AQS的各种实现类中，要么是基于独占模式实现的， 要么是基于共享模式实现的。



在AQS中提供了很多和锁操作相关的方法，如：



+ tryAcquire、tryRelease、acquire、release等。
+ tryAcquireShared、tryReleaseShared、releaseShared、acquireShared等。



如果是独占模式，则需要实现tryAcquire、tryRelease、acquire、release等方法，如ReentrantLock：



![1706941054967-75daa8c3-92d1-4c20-8438-34bf758b83be.png](./img/mQe5Ciry42MuzsMY/1706941054967-75daa8c3-92d1-4c20-8438-34bf758b83be-997307.png)



![1706941064938-8a217efd-4422-4607-a081-a674e79589c7.png](./img/mQe5Ciry42MuzsMY/1706941064938-8a217efd-4422-4607-a081-a674e79589c7-911045.png)



如Semaphore则是实现了tryAcquireShared、tryReleaseShared等方法：



![1706941098539-acd4a92e-ae2f-4649-a086-ac0d6fd4eae2.png](./img/mQe5Ciry42MuzsMY/1706941098539-acd4a92e-ae2f-4649-a086-ac0d6fd4eae2-354571.png)



其中也有tryAcquire的实现，但是也是调用了tryAcquireShared来实现的：



![1706941185066-7229f58a-95ef-421e-9b31-3e3da71e809e.png](./img/mQe5Ciry42MuzsMY/1706941185066-7229f58a-95ef-421e-9b31-3e3da71e809e-923210.png)



### 
在独占模式中，状态通常表示是否被锁定（0表示未锁定，1表示锁定）。在共享模式中，状态可以表示可用的资源数量。



**当需要保证某个资源或一段代码在同一时间内只能被一个线程访问时，独占模式是最合适的选择。如我们经常用的ReentrantLock和ReadWriteLock中的写锁。**

****

**当资源或数据主要被多个线程读取，而写操作相对较少时，共享模式能够提高并发性能。如我们经常使用的Semaphore和CountDownLatch，用来多个线程控制共享资源的。还有ReadWriteLock中的读锁允许多个线程同时读取数据，只要没有线程在写入数据。**



> 更新: 2024-07-08 12:11:18  
> 原文: <https://www.yuque.com/hollis666/dr9x5m/wk1gxv6xgqk0folv>