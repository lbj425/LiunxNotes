### 请详细说明keepalived的故障切换工作原理

这种故障切换是通过VRRP协议来实现的，主节点会按一定的时间间隔发送心跳信息的广播包，告诉备节点自己的存活状态信息，当主节点发生故障时，备节点在一段时间内就收到广播包，从而判断主节点出现故障，因此会调用自身的接管程序来接管主节点的IP资源及服务，当主节点恢复时，备节点会主动释放资源，恢复到接管前的状态，从而来实现主备故障切换

**LVS负载的原理，和Nginx负载有啥区别？**

笔者回答：这个问题我觉得面试官司没问好，正常都会这么问“LVS有哪些负载均衡技术和调度算法?"。我回答就是按我说的这种问法回答的，反正他也频繁点头，当然，笔者回答的可能没有下面我整理出来的那么详细，大概意思我都说明白了。

  LVS是Liunx虚拟服务器的简称，利用LVS提供的负载均衡技术和linux操作系统可实现高性能、高可用的服务器集群，一般LVS都是位于整个集群系统的最前端，由一台或者多台负载调度器（Director Server）组成，分发给应用服务器（Real Server）。它是工作在4层（也就是TCP/IP中的传输层）并且是基于IP负载均衡技术的IPVS模块来实现的，IPVS实现负载均衡机制有三种，分别是NAT、TUN和DR，详述如下：

** VS/NAT：** 即（Virtual Server via Network Address Translation）

也就是网络地址翻译技术实现虚拟服务器，当用户请求到达调度器时，调度器将请求报文的目标地址（即虚拟IP地址）改写成选定的Real Server地址，同时报文的目标端口也改成选定的Real Server的相应端口，最后将报文请求发送到选定的Real Server。在服务器端得到数据后，Real Server返回数据给用户时，需要再次经过负载调度器将报文的源地址和源端口改成虚拟IP地址和相应端口，然后把数据发送给用户，完成整个负载调度过程。

可以看出，在NAT方式下，用户请求和响应报文都必须经过Director Server地址重写，当用户请求越来越多时，调度器的处理能力将称为瓶颈。

** VS/TUN ：**即（Virtual Server via IP Tunneling）

也就是IP隧道技术实现虚拟服务器。它的连接调度和管理与VS/NAT方式一样，只是它的报文转发方法不同，VS/TUN方式中，调度器采用IP隧道技术将用户请求转发到某个Real Server，而这个Real Server将直接响应用户的请求，不再经过前端调度器，此外，对Real Server的地域位置没有要求，可以和Director Server位于同一个网段，也可以是独立的一个网络。因此，在TUN方式中，调度器将只处理用户的报文请求，集群系统的吞吐量大大提高。

** VS/DR：** 即（Virtual Server via Direct Routing）

也就是用直接路由技术实现虚拟服务器。它的连接调度和管理与VS/NAT和VS/TUN中的一样，但它的报文转发方法又有不同，VS/DR通过改写请求报文的MAC地址，将请求发送到Real Server，而Real Server将响应直接返回给客户，免去了VS/TUN中的IP隧道开销。这种方式是三种负载调度机制中性能最高最好的，但是必须要求Director Server与Real Server都有一块网卡连在同一物理网段上。

回答负载调度算法，IPVS实现在八种负载调度算法，我们常用的有四种调度算法（**轮叫调度、加权轮叫调度、最少链接调度、加权最少链接调度**）。一般说了这四种就够了，也不会需要你详细解释这四种算法的。你只要把上面3种负载均衡技术讲明白面试官就对这道问题很满意了。接下来你在简单说下与nginx的区别：

**1、轮询(默认) ** 2. **weight（轮询权值）** 3. **ip_hash**

**LVS的优点：**

- 抗负载能力强、工作在第4层仅作分发之用，没有流量的产生，这个特点也决定了它在负载均衡软件里的性能最强的；无流量，同时保证了均衡器IO的性能不会受到大流量的影响；
- 工作稳定，自身有完整的双机热备方案，如LVS+Keepalived和LVS+Heartbeat；
- 应用范围比较广，可以对所有应用做负载均衡；
- 配置性比较低，这是一个缺点也是一个优点，因为没有可太多配置的东西，所以并不需要太多接触，大大减少了人为出错的几率。

**LVS的缺点：**

- 软件本身不支持正则处理，不能做动静分离，这就凸显了Nginx/HAProxy+Keepalived的优势。
- 如果网站应用比较庞大，LVS/DR+Keepalived就比较复杂了，特别是后面有Windows Server应用的机器，实施及配置还有维护过程就比较麻烦，相对而言，Nginx/HAProxy+Keepalived就简单一点

**Nginx的优点：**

- 工作在OSI第7层，可以针对http应用做一些分流的策略。比如针对域名、目录结构。它的正则比HAProxy更为强大和灵活；
- Nginx对网络的依赖非常小，理论上能ping通就就能进行负载功能，这个也是它的优势所在；
- Nginx安装和配置比较简单，测试起来比较方便；
- 可以承担高的负载压力且稳定，一般能支撑超过几万次的并发量；
- Nginx可以通过端口检测到服务器内部的故障，比如根据服务器处理网页返回的状态码、超时等等，并且会把返回错误的请求重新提交到另一个节点；
- Nginx不仅仅是一款优秀的负载均衡器/反向代理软件，它同时也是功能强大的Web应用服务器。LNMP现在也是非常流行的web环境，大有和LAMP环境分庭抗礼之势，Nginx在处理静态页面、特别是抗高并发方面相对apache有优势；
- Nginx现在作为Web反向加速缓存越来越成熟了，速度比传统的Squid服务器更快，有需求的朋友可以考虑用其作为反向代理加速器；

**Nginx的缺点：**

- Nginx不支持url来检测。
- Nginx仅能支持http和Email，这个它的弱势。
- Nginx的Session的保持，Cookie的引导能力相对欠缺。