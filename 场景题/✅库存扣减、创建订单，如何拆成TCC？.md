# ✅库存扣减、创建订单，如何拆成TCC？

# 典型回答


这是一个比较典型的场景题，考察对TCC的理解。



我们先来回顾一下TCC。



[✅什么是TCC，和2PC有什么区别？](https://www.yuque.com/hollis666/dr9x5m/xhvbak3ouy6xqiml)



所谓TCC，就是把一个操作拆分成Try\Confirm\Cancel三个步骤，并且这三个动作已经不是一个事务了，而是三个不同的事务。



怎么理解上面这句话呢？



Try\Confirm\Cancel分别是三个不同的方法，站在事务参与者的角度，在代码中，每一次调用Try或者Confirm或者Cancel的时候，都会单独开启一个数据库事务（如果数据库支持的话），这就是2PC比较大的区别，2PC从头到尾就一个事务。



那么TCC如何拆呢？其实再看下TCC的定义：



+ **<font style="color:rgb(64, 64, 64);">Try阶段</font>**<font style="color:rgb(64, 64, 64);">：执行业务检查，预留资源</font>
+ **<font style="color:rgb(64, 64, 64);">Confirm阶段</font>**<font style="color:rgb(64, 64, 64);">：若所有Try成功，提交资源</font>
+ **<font style="color:rgb(64, 64, 64);">Cancel阶段</font>**<font style="color:rgb(64, 64, 64);">：若任一Try失败，释放预留资源</font>

<font style="color:rgb(64, 64, 64);"></font>

<font style="color:rgb(64, 64, 64);">那么回到问题上，针对库存扣减，如何拆解成TCC呢？</font>



+ **<font style="color:rgb(64, 64, 64);">Try阶段</font>**<font style="color:rgb(64, 64, 64);">：执行业务检查，预留资源</font>
    - <font style="color:rgb(64, 64, 64);">冻结库存</font>
    - `<font style="color:rgb(64, 64, 64);">update inventory_table set frozen_inventory = frozen_inventory + #{count} where id = xxx</font>`
    - `<font style="color:rgb(64, 64, 64);">冻结库存</font>`<font style="color:rgb(64, 64, 64);"> + 1，用户看到的</font>`<font style="color:rgb(64, 64, 64);">可用库存</font>`<font style="color:rgb(64, 64, 64);"> = </font>`<font style="color:rgb(64, 64, 64);">剩余库存</font>`<font style="color:rgb(64, 64, 64);"> - </font>`<font style="color:rgb(64, 64, 64);">冻结库存</font>`<font style="color:rgb(64, 64, 64);"> ，那么，这就起到了资源预留的作用。</font>
+ **<font style="color:rgb(64, 64, 64);">Confirm阶段</font>**<font style="color:rgb(64, 64, 64);">：若所有Try成功，提交资源</font>
    - <font style="color:rgb(64, 64, 64);">解冻并扣减库存</font>
    - `<font style="color:rgb(64, 64, 64);">update inventory_table set frozen_inventory = frozen_inventory - #{count},saleable_inventory = saleable_inventory - #{count} where id = xxx</font>`
    - `<font style="color:rgb(64, 64, 64);">冻结库存</font>`<font style="color:rgb(64, 64, 64);"> - 1， </font>`<font style="color:rgb(64, 64, 64);">剩余库存</font>`<font style="color:rgb(64, 64, 64);"> - 1，即真正做库存扣减。</font>
+ **<font style="color:rgb(64, 64, 64);">Cancel阶段</font>**<font style="color:rgb(64, 64, 64);">：若任一Try/Confirm失败，释放预留资源</font>
    - <font style="color:rgb(64, 64, 64);">解冻库存</font>
    - `<font style="color:rgb(64, 64, 64);">update inventory_table set frozen_inventory = frozen_inventory - #{count} where id = xxx</font>`
    - `<font style="color:rgb(64, 64, 64);">冻结库存</font>`<font style="color:rgb(64, 64, 64);"> - 1， 即释预留资源</font>
+ **<font style="color:rgb(64, 64, 64);">Cancel阶段</font>**<font style="color:rgb(64, 64, 64);">：若Confirm成功，但是其他参与者失败，需要回滚Confirm操作</font>
    - <font style="color:rgb(64, 64, 64);">回退库存</font>
    - `<font style="color:rgb(64, 64, 64);">update inventory_table set saleable_inventory = saleable_inventory + #{count} where id = xxx</font>`
    - `<font style="color:rgb(64, 64, 64);">剩余库存</font>`<font style="color:rgb(64, 64, 64);"> + 1，即回退库存扣减操作。</font>

<font style="color:rgb(64, 64, 64);"></font>

<font style="color:rgb(64, 64, 64);">针对订单创建，如何拆解成TCC呢？</font>

<font style="color:rgb(64, 64, 64);"></font>

+ **<font style="color:rgb(64, 64, 64);">Try阶段</font>**<font style="color:rgb(64, 64, 64);">：执行业务检查，预留资源</font>
    - <font style="color:rgb(64, 64, 64);">创建订单，但是订单用户不可见，无法支付</font>
    - `<font style="color:rgb(64, 64, 64);">insert into order(id,time,order_id,state) value(1,now(),12345,"INIT") </font>`
    - 创建一个INIT状态的订单，这个状态用户不感知
+ **<font style="color:rgb(64, 64, 64);">Confirm阶段</font>**<font style="color:rgb(64, 64, 64);">：若所有Try成功，提交资源</font>
    - `<font style="color:rgb(64, 64, 64);">update order set state = 'TO_PAY' where id = xxx</font>`
    - 订单状态推荐到待支付状态，这时候用户就能看到这个订单了。可以去做支付了
+ **<font style="color:rgb(64, 64, 64);">Cancel阶段</font>**<font style="color:rgb(64, 64, 64);">：若任一Try/Confirm失败，释放预留资源</font>
    - `<font style="color:rgb(64, 64, 64);">update order set state = 'DISCARD' where id = xxx</font>`
    - 订单废弃掉，废弃的订单无法查看，也无法操作，可以定期清理掉。
+ **<font style="color:rgb(64, 64, 64);">Cancel阶段</font>**<font style="color:rgb(64, 64, 64);">：若Confirm成功，但是其他参与者失败，需要回滚Confirm操作</font>
    - `<font style="color:rgb(64, 64, 64);">update order set state = 'DISCARD' where id = xxx</font>`
    - 订单废弃掉，废弃的订单无法查看，也无法操作，可以定期清理掉。



所以，你在回过头来看前面说TCC是三个事务的说法，是不是就理解，三个不同的SQL，每一个都是单独事务执行的。



PS：这个TCC在我的[项目课中有落地实践](https://www.yuque.com/hollis666/dr9x5m/dgolk0cckpb94sia)，代码+视频+文档。有需要的可以了解下。



> 更新: 2025-03-23 14:44:11  
> 原文: <https://www.yuque.com/hollis666/dr9x5m/elbfrkngg37i842u>