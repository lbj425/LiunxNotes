# Liunx运维学习笔记

## 1.  网络基础类

 [1.1  IP地址](Liunx面试笔记/网络基础类/IP地址.md) 

 [1.2  TCP三次握手](Liunx面试笔记/网络基础类/TCP三次握手.md) 

 [1.3  ISO/OSI七层模型](Liunx面试笔记/网络基础类/ISOOSI七层模型.md) 

## 2.  Linux系统管理类

 [2.1 权限优化](Liunx面试笔记/Liunx系统管理类/权限优化.md) 

 [2.2 备份策略](Liunx面试笔记/Liunx系统管理类/备份策略.md) 

 [2.3 Raid](Liunx面试笔记/Liunx系统管理类/Raid.md)  

 [2.4 资源查看](Liunx面试笔记/Liunx系统管理类/资源查看.md) 

 [2.5 Centos 6 7 开机流程](Liunx面试笔记/Liunx系统管理类/Centos6与7开机流程.md) 

 [2.6 系统优化](Liunx面试笔记/Liunx系统管理类/系统优化.md) 

## 3.  Shell编程类



## 4.  Linux服务管理类



## 5.  数据库管理



------



## Linux运维-经典面试题汇总



### 一、网络基础类面试题：

1、简述ISO/OSI七层模型的分层与作用

2、TCP/IP四层模型与作用？

3、TCP协议与UDP协议工作在哪一层，作用是什么？

4、简述TCP三次握手的过程。

5、简述TCP包头的内容。

6、简述TCP四次挥手的过程。

7、172.22.141.231/26，该IP位于哪个网段？该网段拥有多少可用IP地址？广播地址是什么？

8、简述IP地址的分类。

9、简述私有IP地址的作用。

### 二、Linux系统管理类面试题：

1、简述Linux权限划分原则。

2、当用户user1，对/testdir 目录有写和执行权限时，该目录下的只读文件file1 是否可修改和删除？

3、如果一个系统没有任何的备份策略，请写出一个较为全面合理的备份方案！

4、网站服务器每天产生的日志数量较大，请问如何备份?

5、简述Raid 0、Raid 1、Raid 5的特点与原理。

6、简述Raid 6、Raid 10的特点与原理。

7、软Raid与硬Raid的区别？

8、Linux中有许多系统资源需要监管，请问有哪些命令可以查看？

9、简述CentOS 6.x的启动过程？

10、简述CentOS 7.x的启动过程？

11、如何进行Linux系统优化？

## 三、Shell编程类面试题：

1、有一个b.txt文本(内容如下)，要求将所有域名截取出来，并统计重复域名出现的次数：

```
http://www.baidu.com/index.html 
https://www.4399.com/index.html
http://www.sina.com.cn/1024.html
https://www.4399.com/2048.html
http://www.sina.com.cn/4096.html
https://www.4399.com/8192.html
```

2、统计当前服务器正在连接的IP地址，并按连接次数排序

3、使用循环在/atguigu目录下创建10个txt文件，要求文件名称由6位随机小写字母加固定字符串（_gg）组成，例如：pzjebg_gg.txt。

4、生成随机数字。

5、批量检查多个网站是否可以正常访问，要求使用shell数组实现，检测策略尽量模拟用户真实访问模式。

```
http://www.4399.com
http://www.gulixueyuan.com 
http://www.baidu.com
```

## 四、Linux网络服务类面试题：

1、哪些设置能够提升SSH远程管理的安全等级

2、ssh连接时认证时间过长如何解决？

3、scp和rsync进行远程文件复制有什么区别？

4、请描述通过DHCP服务器获取IP地址的过程。

5、简单描述FTP的主动模式和被动模式的区别？

6、集群环境中，如何保证所有服务器之间的时间误差较小。

7、请描述用户访问网站时DNS的解析过程。

8、解释权威DNS和递归DNS的含义，并描述智能DNS的实现原理。

9、公司里有一台服务器，需要在上面跑两个网站，并且其中一个网站需要更换新域名，请问如何处理？

网站1：www.a.com 网站2：www.b.com（旧）www.d.com（新）

10、简述Apache的三种工作模式？

11、请写出工作中常见的Apache优化策略 

12、有哪些技术可以提高网站的安全和效率？

13、Apache和Nginx各有什么优缺点，应该如何选择？

14、为什么Nginx的并发能力强，资源消耗低？

15、写出几个Nginx的常用模块，并描述其功能。

16、请解释Nginx是如何连接PHP进行页面解析的？

17、请描述Nginx和To m c a t之间的数据传输过程？

18、请写出几个常见的HTTP状态码，并解释出现原因。

## 五、数据库管理类面试题：

1、库表student.report,有3个字段，姓名、学科、成绩，记录如下，根据要求完成SQL语句：

|  Name  | Subject | Result |
| :----: | :-----: | :----: |
|  李白  |  Math   |   95   |
|  杜甫  | English |   83   |
| 李商隐 |  Math   |   79   |
| 白居易 |  Math   |   98   |
| 李清照 | English |   85   |
|  王维  |  Math   |   74   |

  1.1  查询姓李的同学的个数。

  1.2  查询表中数学成绩大于80的前2名同学的名字，并按分数从大到小的顺序排列。

2、MYSQL集群一主多从，主库宕机，如何合理切换到从库，其它从库如何处理？

3、单台MySQL达到性能瓶颈时，如何击碎性能瓶颈？

4、MySQL什么时候创建索引？

5、误操作drop语句导致数据库数据破坏，请给出恢复的实际大体步骤。

6、如何保证Redis能永久保存数据？

7、如何利用Redis对MySQL进行性能优化？

## 基础面试题

[牛客网络基础常考面试题](https://www.nowcoder.com/ta/review-network)

### 1. 进程和线程的区别

进程是资源分配的最小单位，线程是 CPU 调度的最小单位。

- 进程只是维护应用程序所需的各种资源，而线程则是真正的执行实体。
- 进程中除了包含线程之外，还包含有独立的内存体，堆区，BSS 段，数据段，代码段等。
- 不同进程间数据资源很难共享，而多个线程可以很方便地共享进程资源。
- 进程要比线程消耗更多的计算机资源。
- 进程间不会相互影响，一个线程挂掉可能会导致进程挂掉，从而引发其他线程挂掉。

### 2. 输入一个网址后发生了什么

- 输入网址并回车。
- 解析域名获得服务器 IP。
- 根据 IP 建立 TCP 管道。
- 浏览器连接 TCP 管道并发送 HTTP 请求。
- 服务器接收并处理请求。
- 服务器通过 TCP 管道传输 HTML 响应。
- 浏览器处理 HTML 响应，并渲染页面。
- 如果 HTML 内包含图片，CSS，JS 等其他资源，会继续请求其他资源。

详细内容可以参考：

[当你在浏览器中输入 google.com 并且按下回车之后发生了什么？](https://github.com/skyline75489/what-happens-when-zh_CN)

[细说浏览器输入URL后发生了什么](https://segmentfault.com/a/1190000012092552)

