# ✅死锁会导致CPU使用率升高吗？为什么？

# 典型回答


**死锁不会导致升高，甚至可能降低**。因为死锁发生时，涉及的线程会在等待获取锁时被挂起，而不是处于忙碌等待状态。因此，这些线程不会占用CPU资源进行计算，但它们会保持在等待状态，直到死锁被解决。



Talk Is Cheap，Show Me The Code！！！

  
我们可以通过实验验证上面的结论，以下实验在8C16G的物理机上实现。内存total=15g，14g可用，因为有1g是因为Linux内核分配给SLAB了。



编写死锁代码：



```plain
public class Main {
    public static void main(String[] args) {
        int threadCnt = 2000; //多创建一些线程观察CPU使用率更合理
        Object[] locks = new Object[threadCnt];
        for (int i = 0; i < threadCnt; i++) { //初始化线程锁对象
            locks[i] = new Object();
        }

        for (int i = 0; i < threadCnt; i++) {
            //为了产生死锁，我们需要一个线程抢占2把锁，以下代码控制创建时相邻2个线程分别拿到相同的锁
            if (i % 2 == 0) {  //确保前一个线程拿锁顺序：锁1->锁2
                new Thread(new DeadLockTest(locks[i], locks[i + 1])).start(); 
            } else { //确保下一个线程拿锁顺序：锁2->锁1
                new Thread(new DeadLockTest(locks[i], locks[i - 1])).start(); 
            }
        }

    }

    public static class DeadLockTest implements Runnable {
        private final Object lock1;
        private final Object lock2;

        public DeadLockTest(Object lock1, Object lock2) {
            this.lock1 = lock1;
            this.lock2 = lock2;
        }

        @Override
        public void run() {
            synchronized (lock1) {
                System.out.println(Thread.currentThread().getName() + " get Lock:" + lock1); //打印线程名抢到的锁
                try {
                    Thread.sleep(1);//休眠1毫秒保证别的线程有机会拿到下面依赖的锁
                } catch (InterruptedException e) {
                    Thread.currentThread().interrupt();
                }
                System.out.println(Thread.currentThread().getName() + " wait Lock:" + lock2);//打印线程名要拿的锁
                synchronized (lock2) {//以下会由于拿锁顺序不正确，产生死锁
                    System.out.println(Thread.currentThread().getName() + " get Lock:" + lock2);//这里由于死锁不会打印出来
                }
            }
        }
    }
}
```



为了验证死锁线程会不会导致CPU使用率升高，我们需要弄许多线程死锁，这样才能模拟出线上环境业务线程多，并且因为业务代码错误导致的死锁，来观察对CPU的影响。  
运行前的CPU使用率

![](./5.png)

![1706941762023-68c89cfa-7acc-4f1c-9cfc-af572c68d404.png](./img/WPT7QdDHVn4LGYdd/1706941762023-68c89cfa-7acc-4f1c-9cfc-af572c68d404-222377.png)



运行后的CPU使用率

![](./6.png)

![1706941762410-db42db30-00b4-4d76-b4a0-78f1f97bdb02.png](./img/WPT7QdDHVn4LGYdd/1706941762410-db42db30-00b4-4d76-b4a0-78f1f97bdb02-713286.png)

从图中可以看到CPU使用率并没有明显升高，java进程占用的CPU非常低。



`jstack -l`![](./7.png)

![1706941762433-44e7ada9-1bd5-4874-8d85-e103f1c0a67f.png](./img/WPT7QdDHVn4LGYdd/1706941762433-44e7ada9-1bd5-4874-8d85-e103f1c0a67f-345106.png)

选一个Thread1查看一下线程状态：



```plain
jps -l |grep -E '[0-9].Main' |awk '{print $1}' #拿到测试代码Java进程pid

jstack -l <java进程pid>|grep Thread1| awk -v FS='nid=| ' '{print $9}' |xargs printf '%d\n' #提取死锁线程Thread1的线程pid

top -Hp <java进程pid> #查看线程状态
```



![](./8.png)![1706941762473-f1816aff-10fc-4c15-bc04-f24afa6c32f2.png](./img/WPT7QdDHVn4LGYdd/1706941762473-f1816aff-10fc-4c15-bc04-f24afa6c32f2-661042.png)



第一列为线程的pid，可以看到状态列为`S`，代表线程处在`sleeping`状态，因为拿不到锁让出CPU的使用权。  
CPU使率用是统计online-cpu的任务，即任务状态为`running`的任务。所以印证了死锁不会导致CPU使用率升高的结论。之所以线上出现死锁使用率降低，是因为死锁后业务代码无法继续运行，导致使用率会降低。



> 更新: 2024-07-08 12:12:02  
> 原文: <https://www.yuque.com/hollis666/dr9x5m/rk5n7i1ambv44id0>