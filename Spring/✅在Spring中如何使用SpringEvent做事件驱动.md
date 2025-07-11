# ✅在Spring中如何使用Spring Event做事件驱动

# 典型回答


Spring Event是Spring框架中的一种事件机制，它允许不同组件之间通过事件的方式进行通信。Spring框架中的事件机制建立在观察者模式的基础上，允许应用程序中的组件注册监听器来监听特定类型的事件，并在事件发生时执行相应的操作。



Spring Event的使用需要定义以下三个内容：



1. 事件（Event）：事件是一个普通的Java对象，用于封装关于事件发生的信息。通常，事件类会包含一些数据字段，以便监听器能够获取事件的相关信息。
2. 事件发布者（Event Publisher）：事件发布者是负责触发事件并通知所有注册的监听器的组件。
3. 事件监听器（Event Listener）：事件监听器是负责响应特定类型事件的组件。它们实现了一个接口或者使用注解来标识自己是一个事件监听器，并定义了在事件发生时需要执行的逻辑。



### 实现一个Spring Event


假设我们在用户注册成功之后，需要发送一条欢迎短信，那么就可以通过事件来实现。



首先定义一个Event，需要继承ApplicationEvent类。



```c
public class RegisterSuccessEvent extends ApplicationEvent {

    public RegisterSuccessEvent(RegisterInfo registerInfo) {
        super(registerInfo);
    }
}

```



在他的构造方法中，可以定义一个具体的事件内容。



然后再定义一个事件的监听者：



```c

/**
 * 案件中心内部事件监听器
 *
 * @author Hollis
 */
@Component
public class RegisterEventListener {

    @EventListener(RegisterSuccessEvent.class)
    public void onApplicationEvent(RegisterSuccessEvent event) {
        RegisterInfo registerInfo = (RegisterInfo) event.getSource();

        //执行发送欢迎短信的逻辑
    }
}

```





以上这个监听器，在监听到一个RegisterSuccessEvent事件被发出来之后，会调用onApplicationEvent方法，我们就可以在这个方法中实现我们的发送欢迎短信的业务逻辑。



有了监听者，那么发送者也需要定义：



```plain
@Service
public class RegisterService{

  @Autowired
  protected ApplicationContext applicationContext;

	public RegisterResponse register(RegisterInfo registerInfo){

		//用户注册核心代码

  	//发送一个注册完成的事件
    applicationContext.publishEvent(new RegisterSuccessEvent(registerInfo));

  }

}
```

 

在我们的RegisterService中，我们在用户注册成功之后，调用applicationContext.publishEvent即可把我们的注册成功事件广播出去了。



但是需要注意的是，默认情况下，Spring Event的调用时同步调用的。如果想要实现异步调用，也是支持的，最简单的方式就是借助@Async 注解：



修改监听器，增加@Async 注解：



```c

/**
 * 案件中心内部事件监听器
 *
 * @author Hollis
 */
@Component
public class RegisterEventListener {

    @EventListener(RegisterSuccessEvent.class)
    @Async
    public void onApplicationEvent(RegisterSuccessEvent event) {
        RegisterInfo registerInfo = (RegisterInfo) event.getSource();

        //执行发送欢迎短信的逻辑
    }
}

```



并且需要开启对异步的支持，需要在Application.java中增加@EnableAsync

 

但是，一般来说我不建议大家直接用@Async，最好是自定义线程池来实现异步：



[为什么不建议直接使用Spring的@Async](https://www.yuque.com/hollis666/dr9x5m/naw927g44ywpxw4e)

# 扩展知识


## Spring Event带来的好处是什么


1. 代码解耦：通过使用事件机制，组件之间不需要直接互相依赖，从而减少了代码之间的耦合度。这使得代码更易于维护和扩展。



2. 职责清晰：事件机制有助于将应用程序拆分为更小的模块，每个模块只关心要做的事儿，和关心自己需要监听的事件就行了。



3. 异步处理：Spring Event机制支持异步事件处理，这意味着可以将事件的处理分发到不同的线程，提高了系统的响应性。



4. 一对多：Spring Event是观察者模式的一种实现，他的一个事件可以有多个监听者，所以当我们有多个模块之间需要通信时，可以直接发一个事件出去，让监听者各自监听即可。



> 更新: 2024-07-08 12:11:11  
> 原文: <https://www.yuque.com/hollis666/dr9x5m/lgs78ulq6l3cg1qk>