# ✅死循环会导致CPU使用率升高吗？为什么？

# 典型回答
  
**死循环会导致CPU使用率升高**。当代码中出现死循环时，涉及的线程会不断执行循环中的指令而不会退出，因此会持续占用处理器资源。这种情况下，CPU会花费所有可用的时间片去执行这个无尽的循环，导致几乎没有资源剩余来处理其他任务或线程。



Talk Is Cheap，Show Me The Code！！！

  
我们可以通过实验验证上面的结论，以下实验在8C16G的物理机上实现。内存total=15g，14g可用，因为有1g是因为Linux内核分配给SLAB了。



编写死循环代码：



```plain
public class Main {
    public static void main(String[] args) {
        while (true){
            System.out.println(System.currentTimeMillis());//死循环输出系统时间戳，强制产生2个系统调用，可以看到CPU us 和sy 占比都会升高
        }
    }
}
```



没有跑以上代码之前的CPU使用率下图所示，`us`代表用户态1%，`sy`代表内核态0.5%。

![](./2.png)

![1706941762009-c3653c95-3518-404c-9c15-f657619b72e9.png](./img/ZOwL3ur_EmvQECAZ/1706941762009-c3653c95-3518-404c-9c15-f657619b72e9-330947.png)



运行代码后，CPU使用率 `us`和`sy`都有升高，同时进程列表中的java进程CPU使用一列也大幅度升高。



> 注意：俩个java进程，一个是IDEA编译器的，一个是通过IDEA启动的测试代码，由于死循环疯狂在IDEA控制台输出系统时间戳，导致IDEA的CPU使用率也升高了。
>

![](./3.png)![1706941762013-73a722cf-f17c-4fe5-a11f-f2e979082e2f.png](./img/ZOwL3ur_EmvQECAZ/1706941762013-73a722cf-f17c-4fe5-a11f-f2e979082e2f-417278.png)



如果把死循环输出的那一行注释掉，可以看到只有`us`用户态的使用率升高了，同时IDEA的进程使用率不会升高。原因是`System.out.println()`和`System.currentTimeMillis()`都会产生系统调用进入内核态，注释掉代码后，while死循环只是用户态的程序代码，不需要进入内核态了。

![](./4.png)





> 更新: 2024-07-08 12:12:01  
> 原文: <https://www.yuque.com/hollis666/dr9x5m/cgygrzax0kehoeml>