# ✅Zookeeper如何保证数据的一致性？

# 典型回答


zk是一个非常典型的CP的系统，在下面这篇文章中阐述过ZK的AP特性。



[✅Zookeeper是CP的还是AP的？](https://www.yuque.com/hollis666/dr9x5m/lxznb86av97adwt6)



作为一个分布式一致性协调组件，他的主要目标就是保证数据一致性。**他主要的实现原理就是通过ZAB算法来实现强一致性。**ZAB算法是ZooKeeper 自研的一种一致性协议，类似于 Paxos / Raft，但针对其“读多写少”的场景做了优化。



> ZAB的核心思想：
>
> 所有 **写操作**都由 Leader 节点处理并广播给所有 Follower。
>
> 所有节点**按相同顺序**接收并应用写操作，保证数据一致。
>
> 一次写操作必须获得**过半节点（Quorum）确认**才能提交。
>



ZooKeeper 通过 **ZAB 协议 + Leader单节点写入 + Leader选举机制 + 多数写入确认 + 日志快照机制**，确保分布式节点间的**强一致性（顺序一致性）**，即所有节点在任意时刻看到的都是相同的数据状态。  



### 写入（顺序）一致性保障


首先，zk规定了所有的所有的 `create`, `setData`, `delete` 等写请求，都会先发到 **Leader**。Leader会分配全局唯一的事务 ID（zxid），并广播给 Follower。只有当 **超过半数节点写成功** 后，才算提交成功。保证了**全局写入顺序**。



[✅Zookeeper是如何保证创建的节点是唯一的？](https://www.yuque.com/hollis666/dr9x5m/bpbx3ste8amlehv8)



所有 Follower 节点只能处理读请求。写入完成后，所有节点的数据是完全一致的。如果客户端向 Follower 读数据，默认读取的是已提交状态（不强制最新，但始终是一致的）。



ZooKeeper 的节点（ZNode）版本号 `version`、`zxid` 是内置的。可以基于版本号进行原子更新，防止并发写冲突。



### Leader选举机制


[✅Zookeeper是选举机制是怎样的？](https://www.yuque.com/hollis666/dr9x5m/tsfqf463g4mbh41k)



在发生故障或重启时，节点间会进行 Leader 选举（基于 epoch + zxid）。选出数据最全的节点作为Leader，其他节点回滚或追赶日志，与 Leader 同步后再参与投票。系统进入一致状态后才对外服务**。**

****

### 持久化和日志机制


zk的所有事务操作都会持久化到事务日志。数据也会周期性快照到磁盘。节点重启后通过日志恢复，保证崩溃恢复后仍一致。



> 更新: 2025-05-24 13:21:34  
> 原文: <https://www.yuque.com/hollis666/dr9x5m/ihxh5g1t20rkcl2x>