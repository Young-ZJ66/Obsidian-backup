# ✅Git如何回滚代码？reset和revert什么区别？

# 典型回答


Git的代码回滚考察的是纯纯的实操了，根据代码所在的位置不同，回滚的方式也不一样。



一般一个文件要经历几个过程：



本地文件修改 -> commit到分支上 -> push到仓库中



首先，说**本地文件修改**，如果你只是想撤销本地文件的修改并恢复到上一次提交时的状态，可以使用`**git checkout**`命令。例如，如果你想撤销对文件example.txt的修改，可以运行以下命令：`git checkout example.txt`。



如果你的代码本地修改后，使用了git** commit或者push提交到了分支上**，想要撤销这一次的提交的话，那么可以使用`**git revert**`和`**git reset**`命令。



例如，如果你想撤销指定的某一次提交，如这次提交的hash值是abcdefg，可以运行以下命令：`git revert abcdefg`或者 `git reset --hard abcdefg`。





# 扩展知识


## revert和reset的区别


revert和reset都能用来回退git的提交，那么他们的区别是什么呢？



reset的回退比较暴力，是彻底回退到指定的版本。并且执行的本次reset动作也没有产生记录，就像一切都没有发生过一样，如果使用--hard的话，还会把这次提交之后的所有其他提交也都一并清除。



而revert是仅仅撤销指定的那一次修改，对于这次commit之后的commit其实是没有影响的。使用 revert会保留更改历史记录，并且可以反复使用以前的更改。每个撤消提交都会添加到历史记录中，并且必须将其合并到目标分支中。



## reset 的三种模式


reset命令有三种模式，分别是soft、mixed和hard。



+ --soft 模式会重置指针，但不会修改工作目录或索引。这意味着之前的更改仍然存在于工作区中，并且可以重新提交。



+ --mixed 模式是默认模式，它重置指针并更新索引以匹配指定的提交。这将取消索引中的所有更改，但工作目录中的更改将保留。



+ --hard 模式会重置指针，索引和工作区。这意味着所有更改都将永久删除，并且没有办法撤销或恢复这些更改。



> 更新: 2024-07-08 12:11:09  
> 原文: <https://www.yuque.com/hollis666/dr9x5m/oh1ocn2wd0ocxz00>