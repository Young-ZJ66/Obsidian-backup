# ✅什么是COW，如何保证的线程安全？

Copy-On-Write简称COW，是一种用于程序设计中的优化策略。**其基本思路是，从一开始大家都在共享同一个内容，当某个人想要修改这个内容的时候，才会真正把内容Copy出去形成一个新的内容然后再改，这是一种延时懒惰策略。**



从JDK1.5开始Java并发包里提供了两个使用CopyOnWrite机制实现的并发容器,它们是CopyOnWriteArrayList和CopyOnWriteArraySet。CopyOnWrite容器非常有用，可以在非常多的并发场景中使用到。

  
CopyOnWriteArrayList相当于线程安全的ArrayList，CopyOnWriteArrayList使用了一种叫写时复制的方法，当有新元素add到CopyOnWriteArrayList时，先从原有的数组中拷贝一份出来，然后在新的数组做写操作，写完之后，再将原来的数组引用指向到新数组。

  
这样做的好处是我们可以对CopyOnWrite容器进行并发的读，而不需要加锁，因为当前容器不会添加任何元素。所以CopyOnWrite容器也是一种读写分离的思想，读和写不同的容器。

  
**注意：CopyOnWriteArrayList的整个add操作都是在锁的保护下进行的。也就是说add方法是线程安全的。**

  
**CopyOnWrite并发容器用于读多写少的并发场景。**比如白名单，黑名单，商品类目的访问和更新场景。

  
和ArrayList不同的是，它具有以下特性：

  
支持高效率并发且是线程安全的  
因为通常需要复制整个基础数组，所以可变操作（add()、set() 和 remove() 等等）的开销很大  
迭代器支持hasNext(), next()等不可变操作，但不支持可变 remove()等操作  
使用迭代器进行遍历的速度很快，并且不会与其他线程发生冲突。在构造迭代器时，迭代器依赖于不变的数组快照  


若有收获，就点个赞吧

  




> 更新: 2024-07-08 12:11:42  
> 原文: <https://www.yuque.com/hollis666/dr9x5m/sn842t5l24dmlsp4>