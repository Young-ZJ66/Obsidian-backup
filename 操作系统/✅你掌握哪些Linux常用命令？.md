# ✅你掌握哪些Linux常用命令？

# 典型回答
列一下我觉得我们比较常用的Linux命令。_**需要注意的是，本文并不是命令详解，所以并不包含每个命令的所有参数的详细展开介绍，这里只介绍我自己工作中常用的一些用法。相信大家在工作中也基本都是会这么用。如果想要了解具体某个命令，可以单独学习即可。**_

### 系统信息
1. **top**<font style="color:rgb(55, 65, 81);">：实时显示系统进程和资源使用情况。当线上报警CPU占用率过高，load飙高的时候，我们通常会先上去使用top命令看一下具体哪些进程耗费了资源。</font>

<font style="color:rgb(55, 65, 81);"></font>

![1702089650506-29faa34a-9c93-4640-a599-6a9dc37a2f92.png](./img/nqMF2YsQJQiD_rg8/1702089650506-29faa34a-9c93-4640-a599-6a9dc37a2f92-539952.png)

<font style="color:rgb(55, 65, 81);"></font>

2. **df**<font style="color:rgb(55, 65, 81);">：显示磁盘空间使用情况。当线上服务器报警磁盘满的时候，需要上去查看磁盘占用情况，可以使用这个命令</font>



![1702089414016-be73b5d4-3335-4eb1-9dcd-169d45586dff.png](./img/nqMF2YsQJQiD_rg8/1702089414016-be73b5d4-3335-4eb1-9dcd-169d45586dff-208595.png)



**-h**<font style="color:rgb(55, 65, 81);">（--human-readable）：以易于阅读的格式（如MB、GB）显示信息。</font>

![1702089512659-a8c07ae8-d971-41a3-8619-a4aa29110912.png](./img/nqMF2YsQJQiD_rg8/1702089512659-a8c07ae8-d971-41a3-8619-a4aa29110912-260336.png)



3. **du**<font style="color:rgb(55, 65, 81);">：显示目录或文件的磁盘使用量。</font>



这个命令可以查看目录的磁盘占用情况，常用的几个命令如下图：



![1702089959701-271a7939-f7fc-4d05-ad38-6fd0082b340b.png](./img/nqMF2YsQJQiD_rg8/1702089959701-271a7939-f7fc-4d05-ad38-6fd0082b340b-626748.png)



4. <font style="color:rgb(55, 65, 81);">date：</font><font style="color:rgb(51, 51, 51);">查看和设置系统的日期和时间</font>

<font style="color:rgb(51, 51, 51);"></font>

![1702091273463-7cfc9e94-2415-4336-b4b4-d94437966fed.png](./img/nqMF2YsQJQiD_rg8/1702091273463-7cfc9e94-2415-4336-b4b4-d94437966fed-512631.png)



### 系统管理
1. **ps**<font style="color:rgb(55, 65, 81);">：查看当前进程。通常用来查看Java进程的情况以及检查JVM参数：</font>

<font style="color:rgb(55, 65, 81);"></font>

```plain
//查找java进程，相当于jps命令，但是有的时候线上服务器没办法执行jps，可以用以下命令代替
ps aux|grep java
//查询java进程，并高亮显示Xmx参数部分
ps aux|grep java | grep --color Xmx
```



![1702091116260-da1b5700-b93f-4e36-8038-0dc587ff290a.png](./img/nqMF2YsQJQiD_rg8/1702091116260-da1b5700-b93f-4e36-8038-0dc587ff290a-730185.png)

<font style="color:rgb(55, 65, 81);"></font>

2. **kill**<font style="color:rgb(55, 65, 81);">：杀死进程，慎用，尤其是在生产环境中，尤其是kill -9。</font>

[✅对JDK进程执行kill -9有什么影响？](https://www.yuque.com/hollis666/dr9x5m/kmlq81)



3. **chmod**<font style="color:rgb(55, 65, 81);">：更改文件或目录权限。</font>
4. **chown**<font style="color:rgb(55, 65, 81);">：更改文件或目录的所有者和群组。</font>

<font style="color:rgb(55, 65, 81);"></font>

### 文件操作
这里就是一些非常常用的文件操作命令了，每一个都不展开讲了，都比较简单，都是必会的。

1. **ls**<font style="color:rgb(55, 65, 81);">：列出目录内容。当需要显示隐藏文件的时候用</font>`<font style="color:rgb(55, 65, 81);">ls -a</font>`
2. **<font style="color:rgb(55, 65, 81);">ll</font>**<font style="color:rgb(55, 65, 81);">：</font>**ll**<font style="color:rgb(55, 65, 81);">是</font>**ls -l**<font style="color:rgb(55, 65, 81);">命令的一个别名，用于以详细列表格式显示当前目录中的文件和目录。</font>

![1702090099317-9624e98c-bff8-45a0-8570-7a2b42c15366.png](./img/nqMF2YsQJQiD_rg8/1702090099317-9624e98c-bff8-45a0-8570-7a2b42c15366-771659.png)

3. **cd**<font style="color:rgb(55, 65, 81);">：更改当前目录。</font>
4. **pwd**<font style="color:rgb(55, 65, 81);">：显示当前目录路径。</font>
5. **<font style="color:rgb(55, 65, 81);">open</font>**<font style="color:rgb(55, 65, 81);">：直接打开当前文件夹，这个命令在linux中用的不多，但是我在mac中用的比较多，当我在idea中的时候，想要打开当前目录的文件夹，我就会Terminal中使用open命令。这个命令会通过文件管理器打开当前目录。</font>

![1702090447547-f92bb300-a1be-4ce3-8412-fd9393328824.png](./img/nqMF2YsQJQiD_rg8/1702090447547-f92bb300-a1be-4ce3-8412-fd9393328824-423591.png)

6. **mkdir**<font style="color:rgb(55, 65, 81);">：创建新目录。</font>
7. **rmdir**<font style="color:rgb(55, 65, 81);">：删除空目录。</font>
8. **rm**<font style="color:rgb(55, 65, 81);">：删除文件或目录。</font>
9. **cp**<font style="color:rgb(55, 65, 81);">：复制文件或目录。</font>
10. **mv**<font style="color:rgb(55, 65, 81);">：移动或重命名文件或目录。</font>
11. **touch**<font style="color:rgb(55, 65, 81);">：创建空文件或更新文件时间戳。</font>
12. **find**<font style="color:rgb(55, 65, 81);">：搜索文件和目录。find非常好用，介绍下我常见的用法：</font>

```plain
// 在当前目录及其子目录中查找名为filename.txt的文件：
find . -name filename.txt
//查找所有目录
find . -type d
//查找所有普通文件
find . -type f
//查找大于10MB的文件
find . -size +10M
//查找修改时间在过去7天内的.log文件
find . -name "*.log" -mtime -7
```

<font style="color:rgb(55, 65, 81);"></font>

### 日志查看
日志查看是一个非常高频的命令，我常用的日志查看命令有以下这些：

1. **vi/vim：**
2. **cat**<font style="color:rgb(55, 65, 81);">：查看文件内容。</font>用于查看较小的文本文件
3. **more**<font style="color:rgb(55, 65, 81);"> / </font>**less**<font style="color:rgb(55, 65, 81);">：分页查看文件内容。less可以翻页，more不能翻页。查看较大的文本文件。</font>
4. **tail**<font style="color:rgb(55, 65, 81);">：查看文件末尾内</font>容，通常用来实时监视日志文件的新增内容：



```plain
tail -f application.log
//只滚动输出ERROR的日志
tail -f application.log |grep ERROR
```



5. **head**<font style="color:rgb(55, 65, 81);">：查看文件开始部分的内容。用于快速查看文件的开头部分。</font>
6. **grep**<font style="color:rgb(55, 65, 81);">：搜索文件中的文本行，并显示匹配的行。通常用来查找包含特定关键词的日志条目。</font>

<font style="color:rgb(55, 65, 81);"></font>

```plain
//查询日志中有ERROR的行
grep "ERROR" application.log
//查询日志中有ERROR和Biz的行
grep "ERROR" application.log | grep "Biz"
```



### 网络和通信
1. **ping**<font style="color:rgb(55, 65, 81);">：检测网络到另一台主机的连接。</font>
2. **curl**<font style="color:rgb(55, 65, 81);"> / </font>**wget**<font style="color:rgb(55, 65, 81);">：从网络上下载文件。</font>
3. **netstat**<font style="color:rgb(55, 65, 81);">：显示网络连接、路由表、接口统计等信息。</font>
4. **ssh**<font style="color:rgb(55, 65, 81);">：安全远程登录。</font>
5. **scp**<font style="color:rgb(55, 65, 81);">：通过SSH复制远程文件。</font>
6. **telnet：**<font style="color:rgb(55, 65, 81);">主要被用于创建到远程主机的终端会话，或者测试远程主机上特定端口的可达性和服务的响应性。（我之所以这个命令用的多，是因为我们自己的web容器会在本地起一个端口记录我们的应用提供了哪些RPC服务和暴露了哪些RPC服务，所以有时候检查服务的时候需要用到它。）</font>
7. **<font style="color:rgb(55, 65, 81);">ifconfig</font>**<font style="color:rgb(55, 65, 81);">：查看和更改网络接口的配置，例如IP地址、子网掩码和广播地址。有的时候我们需要做远程debug，需要知道远程机器的ip地址，就可以通过这个命令来查看。</font>

<font style="color:rgb(55, 65, 81);"></font>

![1702091439959-72c489fc-cc5f-433e-bb73-54b6142eb70c.png](./img/nqMF2YsQJQiD_rg8/1702091439959-72c489fc-cc5f-433e-bb73-54b6142eb70c-795299.png)



### 压缩与解压
1. **tar**<font style="color:rgb(55, 65, 81);">：压缩和解压tar文件。</font>
2. **gzip**<font style="color:rgb(55, 65, 81);"> / </font>**gunzip**<font style="color:rgb(55, 65, 81);">：压缩和解压gzip文件。</font>
3. **zip**<font style="color:rgb(55, 65, 81);"> / </font>**unzip**<font style="color:rgb(55, 65, 81);">：压缩和解压zip文件。</font>

### 包管理
1. **apt-get**<font style="color:rgb(55, 65, 81);">（Debian系）、</font>**yum**<font style="color:rgb(55, 65, 81);">（RedHat系）：软件包的安装、更新和管理（根据你的Linux发行版而定）。</font>

### Git&Maven
1. **git**<font style="color:rgb(55, 65, 81);">：版本控制工具，常用于代码管理。</font>

```plain
git add 
git fetch
git commit 
git pull
git push
git checkout
git merge
```

<font style="color:rgb(55, 65, 81);"></font>

2. **<font style="color:rgb(55, 65, 81);">maven：</font>**<font style="color:rgb(55, 65, 81);">包管理，仲裁管理</font>



```plain
//删除之前构建生成的所有文件（例如，target目录下的文件）
mvn clean
//将最终的包（如JAR、WAR等）部署到配置的远程仓库
mvn deploy
//先清理项目，然后执行构建并安装到本地仓库，同时跳过测试。
mvn clean install -Dmaven.test.skip=true
//-U参数会强制Maven更新依赖，即检查远程仓库中是否有更新的snapshot版本，并下载更新。
mvn clean install -Dmaven.test.skip=true -U
//生成项目依赖树，并将输出重定向到名为tree的文件
mvn dependency:tree > tree
```



### 系统监控和性能分析
1. **vmstat**<font style="color:rgb(55, 65, 81);">：显示虚拟内存统计信息。</font>
2. **iostat**<font style="color:rgb(55, 65, 81);">：显示CPU和输入/输出统计信息。</font>
3. **dmesg**<font style="color:rgb(55, 65, 81);">：显示内核相关的日志信息。</font>

<font style="color:rgb(55, 65, 81);">掌握这些基本命令可以帮助你更高效地管理和维护Linux环境，对于Java Web开发来说尤其重要。随着经验的积累，你可能还会需要学习更多高级命令和脚本来处理复杂的任务。</font>



> 更新: 2024-07-13 16:02:29  
> 原文: <https://www.yuque.com/hollis666/dr9x5m/uy7orgvls6tbieso>