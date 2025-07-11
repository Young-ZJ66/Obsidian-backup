# ✅JDK1.8和1.9中类加载器有哪些不同

# 典型回答


从Java虚拟机的角度来讲，只存在两种不同的类加载器：一种是启动类加载器（Bootstrap ClassLoader），这个类加载器使用C++语言实现（只限于HotSpot），是虚拟机自身的一部分；



另一种就是所有其他的类加载器，这些类加载器都由Java语言实现，独立于虚拟机外部，并且全都继承自抽象类java.lang.ClassLoader。



从Java开发人员的角度来看，类加载器还可以划分得更细致一些，不过，这里需要区分JDK的版本，在JDK 1.8及之前的版本，和之后的版本是不太一样的。主要是因为JDK 1.9中提供了Jigsaw实现模块化，导致类加载器发生了一些变化。



在JDK1.9中，原来的扩展类加载器被重命名为**平台类加载器—****PlatformClassLoader**<font style="color:rgb(55, 65, 81);"> </font>。它主要加载的是那些属于Java平台模块系统的非核心模块。这些模块在 module-info.java 文件中被明确声明。



### JDK 1.8及之前


JDK 1.8 以前会使用到以下3种系统提供的类加载器。



1. **启动类加载器（Bootstrap ClassLoader**）： 这个类加载器负责将存放在＜JAVA_HOME＞\lib目录中的，或者被-Xbootclasspath参数所指定的路径中的，并且是虚拟机识别的（仅按照文件名识别，如rt.jar，名字不符合的类库即使放在lib目录中也不会被加载）类库加载到虚拟机内存中。启动类加载器无法被Java程序直接引用，用户在编写自定义类加载器时，如果需要把加载请求委派给引导类加载器，那直接使用null代替即可
2. **扩展类加载器（Extension ClassLoader）**： 这个加载器由sun.misc.Launcher$ExtClassLoader实现，它负责加载＜JAVA_HOME＞\lib\ext目录中的，或者被java.ext.dirs系统变量所指定的路径中的所有类库，开发者可以直接使用扩展类加载器。
3. **应用程序类加载器（Application ClassLoader）**： 这个类加载器由sun.misc.Launcher$App-ClassLoader实现。由于这个类加载器是ClassLoader中的getSystemClassLoader()方法的返回值，所以一般也称它为系统类加载器。它负责加载用户类路径（ClassPath）上所指定的类库，开发者可以直接使用这个类加载器，如果应用程序中没有自定义过自己的类加载器，一般情况下这个就是程序中默认的类加载器。



![1704516962330-42578c85-4180-4535-85ff-783e408d7764.png](./img/EgY_kFfi_XJBktc1/1704516962330-42578c85-4180-4535-85ff-783e408d7764-510975.png)



### JDK 1.9及以后


在JDK 9中，类加载器发生了一些变化，原来的扩展类加载器被重命名为**平台类加载器—****PlatformClassLoader**<font style="color:rgb(55, 65, 81);"> </font>。



**PlatformClassLoader** 负责加载JDK平台本身的类库，这些类库位于JDK的 lib 目录下，但不包括核心的 java.* 类库（这些由启动类加载器加载）。它主要加载的是那些属于Java平台模块系统的非核心模块。这些模块在 module-info.java 文件中被明确声明。



![1704518033721-2177d4ef-a79d-4b21-a980-fcac04264cde.png](./img/EgY_kFfi_XJBktc1/1704518033721-2177d4ef-a79d-4b21-a980-fcac04264cde-180748.png)



# 扩展知识


## 类加载器之间的关系


很多人因为知道双亲委派这个词，就以为这些类加载器之间是继承关系，但是其实不是的。他们之间是组合关系。



[✅为什么建议多用组合少用继承？](https://www.yuque.com/hollis666/dr9x5m/yya9secquv5o8dr9)



在ClassLoader类中有一个ClassLoader类型的成员变量，他叫parent，他其实就是代表着当前类的上一层类加载器。



```latex
public abstract class ClassLoader {

    // The parent class loader for delegation
    // Note: VM hardcoded the offset of this field, thus all new fields
    // must be added *after* it.
    private final ClassLoader parent;
}
```



这就是通过组合而不是继承引入进来的，当我们想要把一个类委派给上层类加载加载时，直接调用parent.loadClass即可，如 [代码](https://github.com/zxiaofan/JDK/blob/master/JDK1.8/src/java/lang/ClassLoader.java#L356)：



![1704517868481-46d10fe6-533c-4b85-b072-33d25941e753.png](./img/EgY_kFfi_XJBktc1/1704517868481-46d10fe6-533c-4b85-b072-33d25941e753-373764.png)



> 更新: 2024-07-08 12:11:08  
> 原文: <https://www.yuque.com/hollis666/dr9x5m/mla5wg5f3xwifa1d>