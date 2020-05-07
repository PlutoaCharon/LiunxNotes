[TOC]



## Apache配置

### 虚拟主机

- 基于IP的虚拟主机
- 基于IP+端口的虚拟主机
- 基于域名的虚拟主机

#### 1. 虚拟主机-基于IP

```yaml
<VirtualHost 192.168.100.128:80>
	ServerName www.a.com
	DocumentRoot "/www/a.com/"    #网页路径
</VirtualHost>

<VirtualHost 192.168.100.129:80>
	ServerName www.b.com
	DocumentRoot "/www/b.com/"    #网页路径
</VirtualHost>
```



#### 2. 虚拟主机-基于IP+端口

```yaml
<VirtualHost 192.168.100.128:80>
	ServerName www.a.com
	DocumentRoot "/www/a.com/"    #网页路径
</VirtualHost>

<VirtualHost 192.168.100.128:8080>
	ServerName www.b.com
	DocumentRoot "/www/b.com/"    #网页路径
</VirtualHost>
```



#### 3. 虚拟主机+基于域名

```bash
<VirtualHost *:80>
	ServerName www.a.com
	DocumentRoot "/www/a.com/"    #网页路径
</VirtualHost>

<VirtualHost *:80>
	ServerName www.b.com
	DocumentRoot "/www/b.com/"    #网页路径
</VirtualHost>
```

### rewrite地址重写

1. 虚拟主机能正常访问

2. 修改配置文件

   ```yaml
   <VirtualHost *:80>
   	ServerName www.b.com
   	DocumentRoot "/www/b.com/"  #此处新增跳转指令（见下一页）
   </VirtualHost>
   
   <VirtualHost *:80>#新增虚拟主机（新域名，目录不变）
   	ServerName www.d.com
   	DocumentRoot "/www/b.com/"
   </VirtualHost>
   
   
   <IfModule mod_rewrite.c> #在指定的网站目录下创建文件，并添加以下内容
   	RewriteEngine on # 开启rewrite功能
   	RewriteCond %{HTTP_HOST} ^www.b.com # 把以www.a.com开头的内容赋值给HTTP_HOST变量
   	RewriteRule ^(.*)$ http://www.d.com/$1 [R=permanent,L] 
   	# ^(.*)$ 指代客户端要访问的资源
   	# $1 把.* 所指代的内容赋值到$1变量中
   	# R=permanent 永久重定向= 301
   	# L 指定该规则为最后一条生效的规则，以后的不再生效
   </IfModule>
   ```

   

### 简述Apache的三种工作模式

#### 1. prefork模式

![image-20200507190237023](../../Images/image-20200507190237023.png)

关键字：多进程

`prefork`模式可以算是很古老但是非常稳定的模式。Apache在启动之初，就预派生`fork`一些子进程，然后等待请求进来，并且总是试图保持一些备用的子进程。之所以这样做，是**为了减少频繁创建和销毁进程的开销**。**每个子进程中只有一个线程，在一个时间点内，只能处理一个请求。**

![image-20200507195317910](../../Images/image-20200507195317910.png)

**优点：**成熟，兼容所有新老模块。进程之间完全独立，使得它非常稳定。同时，不需要担心线程安全的问题。

**缺点：**一个进程相对占用更多的系统资源，消耗更多的内存。而且，它并不擅长处理高并发请求，在这种场景下，它会将请求放进队列中，一直等到有可用进程，请求才会被处理。

```yaml
<IfModule mpm_prefork_module>
    #服务器启动时建立的子进程数量
    StartServers          5

    #空闲子进程的最小数量，默认5；
    #如果当前空闲子进程数少于MinSpareServers ，那么Apache将会产生新的子进程。此参数不要设的太大。
    MinSpareServers       5

    #空闲子进程的最大数量，默认10；
    #如果当前有超过MaxSpareServers数量的空闲子进程，那么父进程会杀死多余的子进程。
    #此参数也不需要设置太大，如果你将其设置比 MinSpareServers 小，
    #Apache会自动将其修改为MinSpareServers+1。
    MaxSpareServers      10

    #限定服务器同一时间内客户端最大接入的请求数量，默认是150；
    #任何超过了该限制的请求都要进入等待队列，一旦一个个连接被释放，队列中的请求才将得到服务。
    MaxClients          150

    #每个子进程在其生命周期内允许最大的请求数量，
    #如果请求总数已经达到这个数值，子进程将会结束，如果设置为0，子进程将永远不会结束。
    #若该值设置为非0值，可以防止运行PHP导致的内存泄露。
    MaxRequestsPerChild   0
</IfModule>
```

- 创建的进程数，最多达到每秒32个，直到满足`MinSpareServers`设置的值为止。这就是预派生（`prefork`）的由来。这种模式可以不必在请求到来时再产生新的进程，从而减小了系统开销以增加性能。
- 并发量请求数到达`MaxClients`（如256）时，而空闲进程只有10个。apache为继续增加创建进程。直到进程数到达256个。
- 当并发量高峰期过去了，并发请求数可能只有一个时，apache逐渐删除进程，直到进程数到达`MinSpareServers`为止。

#### 2. worker模式

![image-20200507190247105](../../Images/image-20200507190247105.png)

关键字：多进程 + 多线程

`worker`模式比起上一个，是使用了多进程+多线程的模式。它也预先fork了几个子进程（数量比较少），**每个子进程能够生成一些服务线程和一个监听线程，该监听线程监听接入请求并将其传递给服务线程处理和应答**。

Apache总是试图维持一个备用(spare)或是空闲的服务线程池。这样，客户端无须等待新线程或新进程的建立即可得到处理。线程比起进程会更轻量，因为线程通常会共享父进程的内存空间，因此，内存的占用会减少一些，在高并发的场景下，表现得比 prefork模式好。

##### 为什么不直接使用多线程（即在一个进程内实现多进程），还要引入多进程？

原因主要是需要考虑稳定性，如果一个线程异常挂了，会导致父进程连同其他正常的子线程都挂了（它们都是同一个进程下的）。`多进程+多线程模式`中，各个进程之间都是独立的，如果某个线程出现异常，受影响的只是Apache的一部分服务，而不是整个服务。其他进程仍然可以工作。

优点：占据更少的内存，高并发下表现更优秀。

缺点：必须考虑线程安全的问题，因为多个子线程是共享父进程的内存地址的。如果使用`keep-alive`的长连接方式，也许中间几乎没有请求，这时就会发生阻塞，线程被挂起，需要一直等待到超时才会被释放。如果过多的线程，被这样占据，也会导致在高并发场景下的无服务线程可用。（该问题在prefork模式下，同样会发生）

```yaml
<IfModule mpm_worker_module>
    #服务器启动时建立的子进程数量
    StartServers          2

    #限定服务器同一时间内客户端最大接入的请求数量，默认是150；
    #任何超过了该限制的请求都要进入等待队列，一旦一个个连接被释放，队列中的请求才将得到服务。
    MaxClients          150

    #空闲子进程的最小数量
    MinSpareThreads      25

    #空闲子进程的最大数量
    MaxSpareThreads      75 

    #每个子进程产生的线程数量
    ThreadsPerChild      25

    #每个子进程在其生命周期内允许最大的请求数量，如果请求总数已经达到这个数值，子进程将会结束，
    #如果设置为0，子进程将永远不会结束。将该值设置为非0值，可以防止运行PHP导致的内存泄露。
    MaxRequestsPerChild   0
</IfModule>
```

- 由主控制进程生成`StartServers`个子进程，每个子进程中包含固定的`ThreadsPerChild`线程数，各个线程独立地处理请求。
- 同样，为了尽量避免在请求到来才生成线程，`MinSpareThreads`和`MaxSpareThreads`设置了最少和最多的空闲线程数；而`MaxClients`设置了所有子进程中的线程总数。
- 如果现有子进程中的线程总数不能满足负载，控制进程将派生新的子进程。

#### 3. event模式

![image-20200507190253899](../../Images/image-20200507190253899.png)

关键字：多进程 + 多线程 + epoll

这个是 Apache中最新的模式，在现在版本里的已经是稳定可用的模式。它和 worker模式很像，最大的区别在于，它解决了`keep-alive`场景下 ，长期被占用的线程的资源浪费问题。

`event` MPM中，会有一个专门的线程来管理这些`keep-alive`类型的线程，当有真实请求过来的时候，将请求传递给服务线程，执行完毕后，又允许它释放。这样，一个线程就能处理几个请求了，实现了异步非阻塞。

`event` MPM在遇到某些不兼容的模块时，会失效，将会回退到worker模式，一个工作线程处理一个请求。官方自带的模块，全部是支持`event`MPM的。

```
<IfModule mpm_worker_module>
    #服务器启动时建立的子进程数量
    StartServers             3

    #空闲子进程的最小数量
    MinSpareThreads         75

    #空闲子进程的最小数量
    MaxSpareThreads        250

    #每个子进程产生的线程数量
    ThreadsPerChild         25

    #限定服务器同一时间内客户端最大接入的请求数量，默认是150；
    #任何超过了该限制的请求都要进入等待队列，一旦一个个连接被释放，队列中的请求才将得到服务。
    MaxRequestWorkers      400

    #每个子进程在其生命周期内允许最大的请求数量，如果请求总数已经达到这个数值，子进程将会结束
    #如果设置为0，子进程将永远不会结束。将该值设置为非0值，可以防止运行PHP导致的内存泄露。
    MaxRequestsPerChild   0
</IfModule>
```

### 查看方式：

```bash
httpd -V | grep -i "server mpm"
指定方式：在编译时，在选项中指定，--with-mpm=xxx
```

### 配置文件

Apache的主配置文件：`/etc/httpd/conf/httpd.conf`

默认站点主目录：`/var/www/html/`

```yaml
ServerTokens OS
#在出现错误页的时候是否显示服务器操作系统的名称，ServerTokens Prod为不显示

ServerRoot "/etc/httpd"
#用于指定Apache的运行目录，服务启动之后自动将目录改变为当前目录
#在后面使用到的所有相对路径都是想对这个目录下

User daemon                          # apache的用户，默认为daemon
Group daemon                         # apache的用户，默认为daemon

PidFile run/httpd.pid
#记录httpd守护进程的pid号码，这是系统识别一个进程的方法
#系统中httpd进程可以有多个，但这个PID对应的进程是其他的父进程

Timeout 60
#服务器与客户端断开的时间

KeepAlive Off
#是否持续连接

MaxKeepAliveRequests 100
#表示一个连接的最大请求数

KeepAliveTimeout 15
#断开连接前的时间

<IfModule prefork.c> 
	StartServers       8 
	MinSpareServers    5 
	MaxSpareServers   20 
	ServerLimit      256 
	MaxClients       256 
	MaxRequestsPerChild  4000 
</IfModule>

<IfModule worker.c> 
	StartServers         4 
	MaxClients         300 
	MinSpareThreads     25 
	MaxSpareThreads     75 
	ThreadsPerChild     25 
	MaxRequestsPerChild  0 
</IfModule>

Listen 80
#监听的端口，如有多块网卡，默认监听所有网卡

LoadModule auth_basic_module modules/mod_auth_basic.so 
LoadModule version_module modules/mod_version.so
#启动时加载的模块

Include conf.d/*.conf
#加载的配置文件

#启动服务后转换的身份，在启动服务时通常以root身份，然后转换身份，这样增加系统安全

ServerAdmin root@localhost    #管理员的邮箱，如果出现问题，会在首页显示

#ServerName www.example.com:80

UseCanonicalName Off
#如果客户端提供了主机名和端口，Apache将会使用客户端提供的这些信息来构建自引用URL。
#这些值与用于实现基于域名的虚拟主机的值相同，并且对于同样的客户端可用。
#CGI变量SERVER_NAME和SERVER_PORT也会由客户端提供的值来构建

DocumentRoot "/var/www/html"    # apache的默认web站点目录路径，结尾不要添加斜线
```

注：如果在编译时候不指定，系统默认的是prefork模式；如果需要换成worker模式，需要在编译的时候带上编译参数：`--with-mpm=worker`

## Apache优化

### 日志的轮替

利用apache自带的`rotatelogs`工具进行日志切割，保证单个日志文件不过大

`CustomLog "|/bin/rotatelogs -l /wwwlogs/access_%Y%m%d.log 86400" combined`

### 美化错误页面

可以将404 500等的错误信息页面重定向到网站首页或其他页面，提升用户体验。

```bash
vim httpd.conf

ErrorDocument 404 http://www.a.com
```

### 屏蔽apahce版本等敏感信息

1. 开启子配置文件调用

   ```yaml
   vi httpd.conf
   Include conf/extra/httpd-default.conf #取消注释
   ```

   

2. 修改配置文件中默认显示的信息

   ```yaml
   vi httpd-default.conf
   ServerTokens Prod 显示“Server: Apache”
   ServerTokens Major 显示“Server: Apache/2′′
   ServerTokens Minor 显示“Server: Apache/2.2′′
   ServerTokens Min 显示“Server: Apache/2.2.17′′
   ServerTokens OS 显示“Server: Apache/2.2.17 (Unix)”
   ServerTokens Full 显示“Server: Apache/2.2.17 (Unix) PHP/5.3.5′′
   ```

   

### 配置静态缓存

```yaml
vim httpd.conf
<IfModule mod_expires.c>    	#此模块默认未启用，请手动启用（Load Module）
	ExpiresActive on
	ExpiresByType image/gif "access plus 1 days"
	ExpiresByType image/jpeg "access plus 24 hours"
	ExpiresByType image/png "access plus 24 hours"
	ExpiresByType text/css "now plus 2 hours"
	ExpiresDefault "now plus 0 min"
</IfModule>
#此模块一般写到指定的某一个网站标签中。
```

### 禁止解析PHP

```yaml
vim httpd.conf
#新增目录权限标签
<Directory “/www/a.com/uploads">
	Options FollowSymLinks
	AllowOverride None
	Order allow,deny
	Allow from all
	php_flag engine off 
</Directory>
```

