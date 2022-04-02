# 序言

Nginx功能丰富，可作为HTTP服务器，也可作为反向代理服务器，邮件服务器。支持FastCGI、SSL、Virtual Host、URL Rewrite、Gzip等功能。并且支持很多第三方的模块扩展。

Nginx的稳定性、功能集、示例配置文件和低系统资源的消耗让他后来居上，在全球活跃的网站中有12.18%的使用比率，大约为2220万个网站。

## Nginx常用功能

1、Http代理，反向代理：作为web服务器最常用的功能之一，尤其是反向代理。 

![img](https://images2015.cnblogs.com/blog/398358/201602/398358-20160202133724350-1807373891.jpg)

Nginx在做反向代理时，提供性能稳定，并且能够提供配置灵活的转发功能。Nginx可以根据不同的正则匹配，采取不同的转发策略，比如图片文件结尾的走文件服务器，动态页面走web服务器，只要你正则写的没问题，又有相对应的服务器解决方案，你就可以随心所欲的玩。并且Nginx对返回结果进行错误页跳转，异常判断等。如果被分发的服务器存在异常，他可以将请求重新转发给另外一台服务器，然后自动去除异常服务器。

2、负载均衡

Nginx提供的负载均衡策略有2种：内置策略和扩展策略。内置策略为轮询，加权轮询，Ip hash。扩展策略，就天马行空，只有你想不到的没有他做不到的啦，你可以参照所有的负载均衡算法，给他一一找出来做下实现。

上3个图，理解这三种负载均衡算法的实现

![img](https://images2015.cnblogs.com/blog/398358/201602/398358-20160202133753382-1863657242.jpg)

Ip hash算法，对客户端请求的ip进行hash操作，然后根据hash结果将同一个客户端ip的请求分发给同一台服务器进行处理，可以解决session不共享的问题。 ![img](https://images2015.cnblogs.com/blog/398358/201602/398358-20160201162405944-676557632.jpg)

3、web缓存

Nginx可以对不同的文件做不同的缓存处理，配置灵活，并且支持FastCGI_Cache，主要用于对FastCGI的动态程序进行缓存。配合着第三方的ngx_cache_purge，对制定的URL缓存内容可以的进行增删管理。

4、Nginx相关地址

源码：https://trac.nginx.org/nginx/browser

官网：http://www.nginx.org/

## Nginx配置文件结构

如果你下载好啦，你的安装文件，不妨打开conf文件夹的nginx.conf文件，Nginx服务器的基础配置，默认的配置也存放在此。

在nginx.conf的注释符号位#

nginx文件的结构，这个对刚入门的同学，可以多看两眼。

默认的config 

![img](https://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif) View Code

nginx文件结构

```
...              #全局块

events {         #events块
   ...
}

http      #http块
{
    ...   #http全局块
    server        #server块
    { 
        ...       #server全局块
        location [PATTERN]   #location块
        {
            ...
        }
        location [PATTERN] 
        {
            ...
        }
    }
    server
    {
      ...
    }
    ...     #http全局块
}
```

1、全局块：配置影响nginx全局的指令。一般有运行nginx服务器的用户组，nginx进程pid存放路径，日志存放路径，配置文件引入，允许生成worker process数等。

2、events块：配置影响nginx服务器或与用户的网络连接。有每个进程的最大连接数，选取哪种事件驱动模型处理连接请求，是否允许同时接受多个网路连接，开启多个网络连接序列化等。

3、http块：可以嵌套多个server，配置代理，缓存，日志定义等绝大多数功能和第三方模块的配置。如文件引入，mime-type定义，日志自定义，是否使用sendfile传输文件，连接超时时间，单连接请求数等。

4、server块：配置虚拟主机的相关参数，一个http中可以有多个server。

5、location块：配置请求的路由，以及各种页面的处理情况。

下面给大家上一个配置文件，作为理解，同时也配入我搭建的一台测试机中，给大家示例。 

```
########### 每个指令必须有分号结束。#################
#user administrator administrators;  #配置用户或者组，默认为nobody nobody。
#worker_processes 2;  #允许生成的进程数，默认为1
#pid /nginx/pid/nginx.pid;   #指定nginx进程运行文件存放地址
error_log log/error.log debug;  #制定日志路径，级别。这个设置可以放入全局块，http块，server块，级别以此为：debug|info|notice|warn|error|crit|alert|emerg
events {
    accept_mutex on;   #设置网路连接序列化，防止惊群现象发生，默认为on
    multi_accept on;  #设置一个进程是否同时接受多个网络连接，默认为off
    #use epoll;      #事件驱动模型，select|poll|kqueue|epoll|resig|/dev/poll|eventport
    worker_connections  1024;    #最大连接数，默认为512
}
http {
    include       mime.types;   #文件扩展名与文件类型映射表
    default_type  application/octet-stream; #默认文件类型，默认为text/plain
    #access_log off; #取消服务日志    
    log_format myFormat '$remote_addr–$remote_user [$time_local] $request $status $body_bytes_sent $http_referer $http_user_agent $http_x_forwarded_for'; #自定义格式
    access_log log/access.log myFormat;  #combined为日志格式的默认值
    sendfile on;   #允许sendfile方式传输文件，默认为off，可以在http块，server块，location块。
    sendfile_max_chunk 100k;  #每个进程每次调用传输数量不能大于设定的值，默认为0，即不设上限。
    keepalive_timeout 65;  #连接超时时间，默认为75s，可以在http，server，location块。

    upstream mysvr {   
      server 127.0.0.1:7878;
      server 192.168.10.121:3333 backup;  #热备
    }
    error_page 404 https://www.baidu.com; #错误页
    server {
        keepalive_requests 120; #单连接请求上限次数。
        listen       4545;   #监听端口
        server_name  127.0.0.1;   #监听地址       
        location  ~*^.+$ {       #请求的url过滤，正则匹配，~为区分大小写，~*为不区分大小写。
           #root path;  #根目录
           #index vv.txt;  #设置默认页
           proxy_pass  http://mysvr;  #请求转向mysvr 定义的服务器列表
           deny 127.0.0.1;  #拒绝的ip
           allow 172.18.5.54; #允许的ip           
        } 
    }
} 
```

上面是nginx的基本配置，需要注意的有以下几点：

1、1.$remote_addr 与$http_x_forwarded_for 用以记录客户端的ip地址； 2.$remote_user ：用来记录客户端用户名称； 3.$time_local ： 用来记录访问时间与时区；4.$request ： 用来记录请求的url与http协议；

 5.$status ： 用来记录请求状态；成功是200， 6.$body_bytes_s ent ：记录发送给客户端文件主体内容大小；7.$http_referer ：用来记录从那个页面链接访问过来的； 8.$http_user_agent ：记录客户端浏览器的相关信息；

2、惊群现象：一个网路连接到来，多个睡眠的进程被同事叫醒，但只有一个进程能获得链接，这样会影响系统性能。

3、每个指令必须有分号结束。

## nginx配置之proxy_pass代理路径

nginx作为一个拥有不错性能的反向代理服务器, 其proxy_pass指令配置有以下几点需要注意的情况.

proxy_pass uri; uri是代理的资源路径
proxy_pass指令的代理格式中,字符串uri分为两种情况, 以正斜杠 / 结尾和以非正斜杠结尾.
正斜杠 / 结尾 :
表示绝对路径代理 , 取代匹配的location参数后的匹配路径字符串;
非正斜杠 / 结尾 :
表示相对路径代理 . 此处如果uri表示的是服务器地址, 则代理请求路径中的服务器地址路径部分 ; 如果uri代理的是服务器上的指定资源, 则代理请求路径中的服务器地址和紧接其后的匹配的location参数部分.

分别以一下几个例子说明:

 case1 :

```
location /proxypath/ {
	proxy_pass http://hostname[:port]/;
}
```

访问`http://hostname/proxypath/page.html`时将由地址`http://hostname/page.html`页面代理请求

 case2 :

```
location /proxypath/ {
	proxy_pass http://hostname[:port];
}
```

访问`http://hostname/proxypath/page.html`时将由地址`http://hostname/proxypath/page.html`页面代理请求
 case3 :

```
location /proxypath/ {
	proxy_pass http://hostname[:port]/resourcepath;
}
```

访问`http://hostname/proxypath/page.html`时将由地址`http://hostname/resourcepathpage.html`页面代理请求
 case4 :

```
location /proxypath/ {
	proxy_pass http://hostname[:port]/resourcepath/;
}
```

访问`http://hostname/proxypath/page.html`时将由地址`http://hostname/resourcepath/page.html`页面代理请求





# 基本概念

- 特点：占有内存少，并发能力强，能承受高负载
- 处理静态文件，索引文件以及自动索引，打开文件描述符缓冲
- 无缓存的反向代理，简单的负载均衡和容错
- 模块化的结构
- 支持SSL和TLSSNI

# 安装

- 安装依赖

  ```
  yum -y install gcc zlib zlib-devel pcre-devel openssl openssl-devel
  ```

  

- 安装nginx

- 启动服务器：./nginx

- 查看进程：ps -ef|grep nginx

- 查看防火墙端口：firewall-cmd --list-all

- 开放防火墙端口：sudo firewall-cmd --add-port=80/tcp --permanent

- 重启防火墙：firewall-cmd -reload

# 常用命令

- 打开所在文件夹：cd /usr/local/nginx/sbin
- 查看版本号：./nginx -v
- 启动nginx：./nginx
- 关闭nginx：./nginx -s  stop
- 重新加载nginx：./nginx -s reload

# 配置文件

- 位置：/usr/local/nginx/conf/nginx.conf

  ```
  ########### 每个指令必须有分号结束。#################
  #user administrator administrators;  #配置用户或者组，默认为nobody nobody。
  #worker_processes 2;  #允许生成的进程数，默认为1
  #pid /nginx/pid/nginx.pid;   #指定nginx进程运行文件存放地址
  error_log log/error.log debug;  #制定日志路径，级别。这个设置可以放入全局块，http块，server块，级别以此为：debug|info|notice|warn|error|crit|alert|emerg
  events {
      accept_mutex on;   #设置网路连接序列化，防止惊群现象发生，默认为on
      multi_accept on;  #设置一个进程是否同时接受多个网络连接，默认为off
      #use epoll;      #事件驱动模型，select|poll|kqueue|epoll|resig|/dev/poll|eventport
      worker_connections  1024;    #最大连接数，默认为512
  }
  http {
      include       mime.types;   #文件扩展名与文件类型映射表
      default_type  application/octet-stream; #默认文件类型，默认为text/plain
      #access_log off; #取消服务日志    
      log_format myFormat '$remote_addr–$remote_user [$time_local] $request $status $body_bytes_sent $http_referer $http_user_agent $http_x_forwarded_for'; #自定义格式
      access_log log/access.log myFormat;  #combined为日志格式的默认值
      sendfile on;   #允许sendfile方式传输文件，默认为off，可以在http块，server块，location块。
      sendfile_max_chunk 100k;  #每个进程每次调用传输数量不能大于设定的值，默认为0，即不设上限。
      keepalive_timeout 65;  #连接超时时间，默认为75s，可以在http，server，location块。
  
      upstream mysvr {   
        server 127.0.0.1:7878;
        server 192.168.10.121:3333 backup;  #热备
      }
      error_page 404 https://www.baidu.com; #错误页
      server {
          keepalive_requests 120; #单连接请求上限次数。
          listen       4545;   #监听端口
          server_name  127.0.0.1;   #监听地址       
          location  ~*^.+$ {       #请求的url过滤，正则匹配，~为区分大小写，~*为不区分大小写。
             #root path;  #根目录
             #index vv.txt;  #设置默认页
             proxy_pass  http://mysvr;  #请求转向mysvr 定义的服务器列表
             deny 127.0.0.1;  #拒绝的ip
             allow 172.18.5.54; #允许的ip           
          } 
      }
  }
  ```

  

- 组成

  - 全局块：影响服务器整体运行

    ```
    #user administrator administrators;  #配置用户或者组，默认为nobody nobody。
    #worker_processes 2;  #允许生成的进程数，默认为1
    #pid /nginx/pid/nginx.pid;   #指定nginx进程运行文件存放地址
    error_log log/error.log debug;  #制定日志路径，级别。这个设置可以放入全局块，http块，server块，级别以此为：debug|info|notice|warn|error|crit|alert|emerg
    ```

    

  - events块：影响服务器与用户的网络连接

    ```
    events {
        accept_mutex on;   #设置网路连接序列化，防止惊群现象发生，默认为on
        multi_accept on;  #设置一个进程是否同时接受多个网络连接，默认为off
        #use epoll;      #事件驱动模型，select|poll|kqueue|epoll|resig|/dev/poll|eventport
        worker_connections  1024;    #最大连接数，默认为512
    }
    ```

    

  - http块：可以包含多个server块

    - http全局块：

      ```
      include       mime.types;   #文件扩展名与文件类型映射表
          default_type  application/octet-stream; #默认文件类型，默认为text/plain
          #access_log off; #取消服务日志    
          log_format myFormat '$remote_addr–$remote_user [$time_local] $request $status $body_bytes_sent $http_referer $http_user_agent $http_x_forwarded_for'; #自定义格式
          access_log log/access.log myFormat;  #combined为日志格式的默认值
          sendfile on;   #允许sendfile方式传输文件，默认为off，可以在http块，server块，location块。
          sendfile_max_chunk 100k;  #每个进程每次调用传输数量不能大于设定的值，默认为0，即不设上限。
          keepalive_timeout 65;  #连接超时时间，默认为75s，可以在http，server，location块。
      
          upstream mysvr {   
            server 127.0.0.1:7878;
            server 192.168.10.121:3333 backup;  #热备
          }
          error_page 404 https://www.baidu.com; #错误页
      ```

      

    - server块：每个server块就相当于一个虚拟主机，一个server可包含多个location

      ```
          server {
              keepalive_requests 120; #单连接请求上限次数。
              listen       4545;   #监听端口
              server_name  127.0.0.1;   #监听地址       
              location  ~*^.+$ {       #请求的url过滤，正则匹配，~为区分大小写，~*为不区分大小写。
                 #root path;  #根目录
                 #index vv.txt;  #设置默认页
                 proxy_pass  http://mysvr;  #请求转向mysvr 定义的服务器列表
                 deny 127.0.0.1;  #拒绝的ip
                 allow 172.18.5.54; #允许的ip           
              } 
          }
      ```

      

    

# 配置实例

#### 正向代理

- 客户端配置了正向代理服务器来访问internet

#### 反向代理

- 服务器使用了反向代理，客户端访问反向代理

- 直接转发

  ```
  location / {
  			proxy_pass	http://127.0.0.1:3000/;
          }
  ```

  

- 根据路径名转发

  ```
  location ~ /nav/ {
  			proxy_pass	http://127.0.0.1:3000/;
          }
  location ~ /api/ {
  			proxy_pass	http://127.0.0.1:4000/;
          }
  ```

  

#### 负载均衡

- 反向代理服务器将客户端的多个请求分发到多个服务器上

  ```
  http {
  ...
  	upstream myserver{
  		ip_hash;
  		server 115.28.52.63:8080 weight=1;
  		server 115.28.52.63:8080 weight=1;
  		fair;
  	}
  ...	
  	server{
  		location / {
  			...
  			proxy_pass http://myserver;
  			proxy_connect_timeout 10;
  		}
  	}
  }
  ```

  

- 分配策略：

  - 轮询（默认）：每个请求按时间顺序逐一分配到不同的后端服务器，如果后端服务器down掉则自动剔除
  - weight：权重，默认为1，权重越高被分配的客户端越多
  - ip_hash：每个请求按访问IP的hash分配，则每个访客固定访问一个后端服务器，可解决session问题
  - fair（第三方）：按后端服务器的响应时间来分配请求，响应时间越短的优先分配

#### 动静分离

- 将动态资源和静态资源分别放置在不同服务器
- 两种方案
  - （最优）动态服务器和静态服务器分离
  - 动态和静态文件混合在一起，通过nginx分开

#### 高可用集群

- 当主nginx服务器宕机后自动使用备份nginx服务器
- 用keepalived软件把主nginx和备份nginx的ip绑定到一个虚拟的ip上，并且keepalived自动监控是否宕机

# nginx原理

- master和worker