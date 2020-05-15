# Liunx运维技能点

## 1.  网络基础类

1. ​       OSI7层模型（TCP4层）

   - ​         [ISOOSI7层模型与TCP/IP协议](Liunx面试笔记/网络基础类/ISOOSI七层模型.md) 
   - ​         [URL到页面的过程](Liunx面试笔记/网络基础类/url到页面的过程.md) 

2. ​       HTTP 

   - ​         [http/https 1.0、1.1、2.0 的区别](Liunx面试笔记/网络基础类/HTTP1，1.1，2的区别.md) 
   - ​         [get/post 以及幂等性](Liunx面试笔记/网络基础类/GET与POST区别.md) 
   - ​         [HTTP 协议头相关](Liunx面试笔记/网络基础类/HTTP与HTTPS.md) 
   - ​         [HTTP与HTTPS区别](Liunx面试笔记/网络基础类/HTTP与HTTPS.md) 
   - ​         [网络攻击（CSRF、XSS、SQL注入）](https://blog.csdn.net/beauty5188/article/details/79558809)
   - ​         [HTTP状态码](Liunx面试笔记/Linux服务管理类/HTTP状态码.md) 

3. ​       TCP/IP       

   - ​         [三次握手、四次挥手](Liunx面试笔记/网络基础类/TCP三次握手.md)                 
   - ​         [拥塞控制（过程、阈值）](https://network.51cto.com/art/202004/614800.htm)     
   - ​         [流量控制与滑动窗口](https://network.51cto.com/art/202004/614800.htm)                
   - ​         [TCP与UDP比较](https://juejin.im/post/5c6fbf54f265da2db718216a)              
   - ​         [子网划分](Liunx面试笔记/网络基础类/IP地址.md)                             
   - ​         [IP地址](Liunx面试笔记/网络基础类/IP地址.md) 
   - ​         [TCP头部检验](Liunx面试笔记/网络基础类/TCP头部检验.md) 
   - ​         [ping 过程中发生了什么](Liunx面试笔记/网络基础类/ping 过程中发生了什么.md) 

4. ​       (B)IO/NIO/AIO       

   - ​         三者原理，各个语言是怎么实现的                
   - ​         Netty                
   - ​         Linux内核select poll epoll               

## 2.  Linux系统管理类

 [2.1 权限优化](Liunx面试笔记/Liunx系统管理类/权限优化.md) 

 [2.2 备份策略](Liunx面试笔记/Liunx系统管理类/备份策略.md) 

 [2.3 Raid](Liunx面试笔记/Liunx系统管理类/Raid.md)  

 [2.4 资源查看](Liunx面试笔记/Liunx系统管理类/资源查看.md) 

 [2.5 Centos 6 7 开机流程](Liunx面试笔记/Liunx系统管理类/Centos6与7开机流程.md) 

 [2.6 系统优化](Liunx面试笔记/Liunx系统管理类/系统优化.md) 

## 3.  Linux服务管理类

 [3.1 SSH服务](Liunx面试笔记/Linux服务管理类/SSH服务.md) 

 [3.2 DHCP+FTP](Liunx面试笔记/Linux服务管理类/DHCP+FTP.md) 

 [3.3 DNS服务](Liunx面试笔记/Linux服务管理类/DNS服务.md) 

 [3.4 Apache](Liunx面试笔记/Linux服务管理类/Apache.md) 

 [3.5 Nginx](Liunx面试笔记/Linux服务管理类/Nginx.md) 

LVS

## 4.  数据库管理

1. ​       索引（包括分类及优化方式，失效条件，底层结构）
2. ​       sql语法（join，union，子查询，having，group by）            
3. ​       引擎对比（InnoDB，MyISAM）
4. ​       数据库的锁（行锁，表锁，页级锁，意向锁，读锁，写锁，悲观锁，乐观锁，以及加锁的select sql方式）            
5. ​       隔离级别，依次解决的问题（脏读、不可重复读、幻读）            
6. ​       事务的ACID            
7. ​       B树、B+树            
8. ​       优化（explain，慢查询，show profile）            
9. ​       数据库的范式
10. ​       分库分表，主从复制，读写分离。            
11. ​       Nosql相关（redis和mem***d区别之类的，如果你熟悉redis，redis还有一堆要问的）           

 [4.1 SQL语句](Liunx面试笔记/数据库/SQL语句.md) 

 [4.2 Mysql主从复制](Liunx面试笔记/数据库/Mysql主从复制.md) 

 [4.3 Mysql索引](Liunx面试笔记/数据库/Mysql索引.md) 

 [4.4 Redis](Liunx面试笔记/数据库/Redis.md) 

## 5.  算法和数据结构     

1. ​       数组、**链表、二叉树**、队列、栈的各种操作（性能，场景）            
2. ​       二分查找和各种变种的二分查找            
3. ​       各类排序算法以及复杂度分析（**快排、归并、堆**）            
4. ​       各类算法题（手写）
5. ​       理解并可以分析时间和空间复杂度
6. ​       动态规划、贪心
7. ​       红黑树、AVL树、Hash树、Tire树、B树、B+树。            
8. ​       图算法（比较少，也就两个最短路径算法理解吧）           

## 6.  操作系统

1. ​       进程通信IPC（几种方式），与线程区别 
2. ​       OS的几种策略（页面置换，进程调度等，每个里面有几种算法）            
3. ​       互斥与死锁相关的            
4. ​       linux常用命令（问的时候都会给具体某一个场景）            
5. ​       Linux内核相关（select、poll、epoll）
6. ​       [进程与线程](Liunx面试笔记/操作系统/进程与线程.md) 
7. ​       协程和线程的区别
8. ​       [僵尸进程孤儿进程](https://www.cnblogs.com/Anker/)

## 7.  自动化

1. ​       [PXE](https://blog.51cto.com/13670314/2164086)

## 8.  编程语言

1. ​       Python语言
   -  [Python垃圾回收与内存管理](Liunx面试笔记/编程语言/Python/Python垃圾回收与内存管理.md) 
   - [深入理解Python中的元类(metaclass)](https://www.cnblogs.com/JetpropelledSnake/p/9094103.html)
   - [@staticmethod和@classmethod的作用与区别](https://blog.csdn.net/handsomekang/article/details/9615239)
   - 
2. ​       Golang语言
   - 
3. ​        Shell语言
   - 



## 8.  Docker

- [Doker网络](https://juejin.im/post/5c3363bf6fb9a049e2322cdb)
- 

## 9.  Kubernetes

- [Kubernetes总结](http://yaoguais.github.io/article/golang/k8sinterview.html)
- 

## 10.  项目

[ElasticSearch脑裂](https://www.cnblogs.com/kevingrace/p/12433503.html)

[ElasticSearch](https://www.cnblogs.com/aspirant/p/11323890.html)

------



## Linux运维-经典面试题汇总

[牛客网络基础常考面试题](https://www.nowcoder.com/ta/review-network)

[Liunx常见面试题](https://www.linuxba.com/?s=面试)

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

### 三、Shell编程类面试题：

1、有一个b.txt文本(内容如下)，要求将所有域名截取出来，并统计重复域名出现的次数：

```
http://www.baidu.com/index.html 
https://www.4399.com/index.html
http://www.sina.com.cn/1024.html
https://www.4399.com/2048.html
http://www.sina.com.cn/4096.html
https://www.4399.com/8192.html
```

答案:

```bash
cat b.txt | cut -d "/" -f 3 | sort | uniq -c | sort –nr 
```

> cut -d 按照分隔符分割 -f 3 截取第三列
>
> uniq -c 显示该行重复次数
>
> sort -nr 按照数字从大到小排列

2、统计当前服务器正在连接的IP地址，并按连接次数排序

3、使用循环在/test目录下创建10个txt文件，要求文件名称由6位随机小写字母加固定字符串（_gg）组成，例如：pzjebg_gg.txt。

```shell
#!/bin/bash 
if [ ! -d /atguigu ] #判断测试目录是否建立
then 
	mkdir /test
fi 
cd /test #进入测试目录
for (( i=1;i<=10;i++ )) #循环10次，每次循环建立6位随机数文件
do 
	filename=$(tr -dc 'A-Za-z0-9' < /dev/urandom | head -c 6)
	touch "$filename"_gg.txt 
done
```



4、生成随机数字。

5、批量检查多个网站是否可以正常访问，要求使用shell数组实现，检测策略尽量模拟用户真实访问模式。

```
http://www.4399.com
http://www.gulixueyuan.com 
http://www.baidu.com
```

```shell
#!/bin/bash
web=(
http://www.4399.com
http://www.gulixueyuan.com 
http://www.baidu.com
1.1.1.1
) #定义数组

for i in ${web[*]}#按照数组中值的个数循环，每次循环把数组中值赋予变量i
do         
	code=$( curl -o /dev/null -s --connect-timeout 5 -w ‘%{http_code}’  $i | grep -E “200|302” )#检测curl状态码
    if [ “$code” != “” ]#变量$code值不为空，则证明网页可以访问        
    then                 
    	echo "$i is ok" >> /root/ok.log        
    else  #变量$code值为空，则休眠10秒，重新检测                
    	sleep 10                 
    	code=$( curl -o /dev/null -s --connect-timeout 5 -w '%{http_code}' $i | grep -E "200|302" )
    	if [ "$code" != "" ]                
    	then                         
    		echo "$i is ok" >> /root/ok.log                
    	else                        
    	echo "$i is error" >> /root/error.log                
    	fi        
    fi
done
```



### 四、Linux网络服务类面试题：

1、哪些设置能够提升SSH远程管理的安全等级

> 1. 登录验证模式修改为密钥登录
> 2. 登录端口修改为非22端口以及指定监听IP
> 3. 禁止root用户远程登录
> 4. 设置无操作时自动断开连接设置
> 5. 登录失败后登录尝试次数为6次
> 6. 编写防火墙规则，使用白名单机制放行ssh服务的监听端口

2、ssh连接时认证时间过长如何解决？

DNS反向解析请求时间过长，以检查此主机名是否与其IP地址真实对应

```bash
配置文件：/etc/ssh/sshd_config

#UseDns yes     修改为no   #取消ssh登录时的dns反向解析请求功能

注意事项：在/etc/ssh/sshd_config配置文件中注释掉的选项不代表不生效，反而代表默认生效，想关闭某功能，一定要取消注释然后修改为no才可以。
```



3、scp和rsync进行远程文件复制有什么区别？

|       |                    |                    |            |                            |
| :---: | :----------------: | :----------------: | :--------: | :------------------------: |
|  scp  |      全量备份      |     文件级传输     |  加密传输  |         资源消耗低         |
| rsync | 差异对比，增量备份 | 分块校验，部分传输 | 非加密传输 | 资源消耗高（零散文件较多） |

4、请描述通过DHCP服务器获取IP地址的过程。

5、简单描述FTP的主动模式和被动模式的区别？

6、集群环境中，如何保证所有服务器之间的时间误差较小。

```
手动测试同步：ntpdate 时间服务器IP地址
自动同步：可以将命令写入计划任务
```

7、请描述用户访问网站时DNS的解析过程。

8、解释权威DNS和递归DNS的含义，并描述智能DNS的实现原理。

```
权威DNS是经上一级授权对域名进行解析的DNS服务器，同时它可以把解析授权转授给其他服务器
递归DNS负责接受用户对任何域名的查询，并返回结果给用户，它可以缓存结果避免用户再向上查询

智能DNS就是将对用户发起的查询进行判断出是哪个运营商的用户查询，然后将请求转发给相应的运营商IP处理，减少跨运营访问的时间，提高访问速度
```



9、公司里有一台服务器，需要在上面跑两个网站，并且其中一个网站需要更换新域名，请问如何处理？

```
网站1：www.a.com 

网站2：www.b.com（旧）www.d.com（新）
```

10、简述Apache的三种工作模式？

11、请写出工作中常见的Apache优化策略 

```txt
设置Apache的日志轮替和切割规则，防止日志过大
美化错误页面，将错误页面重定向到首页或指定页面
屏蔽Apache的版本等信息，防止别人获取Apache的相应版本
配置静态缓存，减少对服务器的访问压力
禁止解析指定目录下的页面程序，比如upload，禁止解析用户上传的脚本文件
```



12、有哪些技术可以提高网站的安全和效率？

13、Apache和Nginx各有什么优缺点，应该如何选择？

14、为什么Nginx的并发能力强，资源消耗低？

15、写出几个Nginx的常用模块，并描述其功能。

16、请解释Nginx是如何连接PHP进行页面解析的？

17、请描述Nginx和Tomcat之间的数据传输过程？

18、请写出几个常见的HTTP状态码，并解释出现原因。

### 五、数据库管理类面试题：

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

```sql
select count(*) from student.report where Nmae like '李%'
```



  1.2  查询表中成绩大于80的前2名同学的名字，并按分数从大到小的顺序排列。

```sql
select Result from report ORDER BY Restult DESC limit 2
```

2、MYSQL集群一主多从，主库宕机，如何合理切换到从库，其它从库如何处理？

3、单台MySQL达到性能瓶颈时，如何击碎性能瓶颈？

4、MySQL什么时候创建索引？

5、误操作drop语句导致数据库数据破坏，请给出恢复的实际大体步骤。

```
手动切割binlog日志并记好切割好的binlog日志文件位置，这里假设为009，备份全部binlog日志
找到之前全备数据最后备份到的binlog文件位置并记好位置，这里假设为005
用mysqladmin命令将005到008binlog文件中的SQL语句分离出来，并找到drop库的语句将其删掉
将之前全备数据导入mysql服务器
将步骤3中分离出的SQL语句导入mysql服务器
将009binlog文件删除，再次刷新binlog日志，到此数据库已恢复成功
```

6、如何保证Redis能永久保存数据？

7、如何利用Redis对MySQL进行性能优化？



