## 第一次建站遇到的坑

#### 购买云服务器

- 选错云服务器系统windows，又自己重装了centos
- 

#### 域名购买、实名和备案

- 不知道哪个先后，一搜一大堆文章都讲的乱七八糟
- 原来要先购买域名（.com的50RMB），再上传身份证照片实名制
- 然后等验证通过后，下载域名证书去备案
- 备案通过才能使用域名以及域名解析

#### 服务器环境搭建

- 看项目和用途选择apache还是nginx
- web选择nginx
- 我的项目是node.js+mongodb后端，vue/react前端

#### 安装

- 最好先安装node，然后可以用命令安装其他



#### nginx配置

- 代理路径匹配简直坑

  ```
  location /proxypath/ {
  	proxy_pass http://hostname[:port]/;
  }
  ```

  代理页面是` http://hostname/page.html `

  ```
  location /proxypath/ {
  	proxy_pass http://hostname[:port];
  }
  ```

  代理页面是` http://hostname/proxypath/page.html `

  害我到处查，简直要命头都大了



## centos服务器配置流程

#### 更新yum源

下载阿里云yum源

```bash
curl -o /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo;
```

更新cache

```bash
yum makecache;
```

查看更新

```bash
yum -y update;
```

#### 安装nodejs

- 去<https://github.com/nodesource/distributions>查看安装说明

  ```
  curl -sL https://rpm.nodesource.com/setup_10.x | bash -
  ```

  ```
  yum install -y nodejs
  ```

  - 注意是nodejs不是node.js

- npm i -g yarn pm2 nodemon
  - yarn：安装包
  - pm2：在生产端让nodejs持续运行
  - nodemon：更新后自动加载



#### 安装mongodb

1. 创建仓库文件: 

```
`vi /etc/yum.repos.d/mongodb-org-3.4.repo`
```

 然后复制下面配置,保存退出

```
`[mongodb-org-3.4]``name=MongoDB Repository``baseurl=https:``//repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.4/x86_64/``gpgcheck=1``enabled=1``gpgkey=https:``//www.mongodb.org/static/pgp/server-3.4.asc`
```

2. yum安装

```
`yum install -y mongodb-org`
```

 没有权限就在前面加:  sudo

安装完毕后修改配置文件:

```
`vi /etc/mongod.conf`
```

 

修改配置文件的 `bind_ip,` 默认是 `127.0.0.1 只限于本机连接`。所以安装完成后必须把这个修改为 0.0.0.0 ,否则通过别的机器是没法连接的!

3. 启动、停止、重启

MongoDB默认将数据文件存储在`/var/lib/mongo`目录，默认日志文件在`/var/log/mongodb`中。如果要修改,可以在 `/etc/mongod.conf` 配置中指定备用日志和数据文件目录。

启动命令:

```
`service mongod start`
```

 停止命令:

```
`service mongod stop`
```

 重启命令:

```
`service mongod stop`
```

查看mongoDB是否启动成功:

可以通过查看日志文件

```
`cat /``var``/log/mongodb/mongod.log`
```

 日志文件应该会出现如下一句说明

```
[initandlisten] waiting for connections on port <port>
```

<port> 是mongodb运行端口

也可以通过下面命令检查是否启动成功

```
`chkconfig mongod ``on`
```

4. 使用

```
`[root@instance-d0nk2r2c ~]# mongo` `## 查看数据库``> show dbs;` `## 查看数据库版本``> db.version();` `## 常用命令帮助``> db.help();`
```

5. 卸载移除mongo

```
`yum erase $(rpm -qa | grep mongodb-org)`
```

6. 移除数据库文件和日志文件

```
`rm -r /``var``/log/mongodb``rm -r /``var``/lib/mongo`
```

 

## pm2

在网上找到pm2.目前似乎最常见的线上部署nodejs项目的有forever,pm2这两种。
使用场合:

- forever管理多个站点，每个站点访问量不大，不需要监控。
- pm2 网站访问量比较大,需要完整的监控界面。

## PM2的主要特性:

- 内建负载均衡（使用Node cluster 集群模块）
- 后台运行
- 0秒停机重载，我理解大概意思是维护升级的时候不需要停机.
- 具有Ubuntu和CentOS 的启动脚本
- 停止不稳定的进程（避免无限循环）
- 控制台检测
- 提供 HTTP API
- 远程控制和实时的接口API ( Nodejs 模块,允许和PM2进程管理器交互 )

## 安装

```
npm install -g pm2
```

## 用法

`$ npm install -g pm2` 命令行全局安装pm2
`$ pm2 start app.js 或者 pm2 start bin/www ` 启动node项目

$ pm2 stop bin/www 停止pm2服务
`$ pm2 list` 列出由pm2管理的所有进程信息，还会显示一个进程会被启动多少次，因为没处理的异常。

![img](https://upload-images.jianshu.io/upload_images/615807-a7d5d4ad8debcf34.png?imageMogr2/auto-orient/strip%7CimageView2/2)


`$ pm2 monit` 监视每个node进程的CPU和内存的使用情况

![img](https://upload-images.jianshu.io/upload_images/615807-1560d7993bbfc87e.png?imageMogr2/auto-orient/strip%7CimageView2/2)


`$ pm2 logs` 显示所有进程日志
`$ pm2 stop all` 停止所有进程
`$ pm2 restart all` 重启所有进程
`$ pm2 reload all` 0秒停机重载进程 (用于 NETWORKED 进程)
`$ pm2 stop 0` 停止指定的进程
`$ pm2 restart 0` 重启指定的进程
`$ pm2 startup` 产生 init 脚本 保持进程活着
`$ pm2 web` 运行健壮的 computer API endpoint ([http://localhost:9615](http://localhost:9615/))
`$ pm2 delete 0` 杀死指定的进程
`$ pm2 delete all` 杀死全部进程

运行进程的不同方式：
`$ pm2 start app.js -i max` 根据有效CPU数目启动最大进程数目
`$ pm2 start app.js -i 3` 启动3个进程
`$ pm2 start app.js -x` 用fork模式启动 app.js 而不是使用 cluster
`$ pm2 start app.js -x -- -a 23` 用fork模式启动 app.js 并且传递参数 (-a 23)
`$ pm2 start app.js --name serverone` 启动一个进程并把它命名为 serverone
`$ pm2 stop serverone` 停止 serverone 进程
`$ pm2 start app.json` 启动进程, 在 app.json里设置选项
`$ pm2 start app.js -i max -- -a 23` 在--之后给 app.js 传递参数
`$ pm2 start app.js -i max -e err.log -o out.log` 启动 并 生成一个配置文件

## 配置pm2启动文件

在项目根目录添加一个processes.json：
内容如下:

```
{
  "apps": [
    {
      "name": "mywork",
      "cwd": "/srv/node-app/current",
      "script": "bin/www",
      "log_date_format": "YYYY-MM-DD HH:mm Z",
      "error_file": "/var/log/node-app/node-app.stderr.log",
      "out_file": "log/node-app.stdout.log",
      "pid_file": "pids/node-geo-api.pid",
      "instances": 6,
      "min_uptime": "200s",
      "max_restarts": 10,
      "max_memory_restart": "1M",
      "cron_restart": "1 0 * * *",
      "watch": false,
      "merge_logs": true,
      "exec_interpreter": "node",
      "exec_mode": "fork",
      "autorestart": false,
      "vizion": false
    }
  ]
}
```

说明:

- apps:json结构，apps是一个数组，每一个数组成员就是对应一个pm2中运行的应用
- name:应用程序名称
- cwd:应用程序所在的目录
- script:应用程序的脚本路径
- log_date_format:
- error_file:自定义应用程序的错误日志文件
- out_file:自定义应用程序日志文件
- pid_file:自定义应用程序的pid文件
- instances:
- min_uptime:最小运行时间，这里设置的是60s即如果应用程序在60s内退出，pm2会认为程序异常退出，此时触发重启max_restarts设置数量
- max_restarts:设置应用程序异常退出重启的次数，默认15次（从0开始计数）
- cron_restart:定时启动，解决重启能解决的问题
- watch:是否启用监控模式，默认是false。如果设置成true，当应用程序变动时，pm2会自动重载。这里也可以设置你要监控的文件。
- merge_logs:
- exec_interpreter:应用程序的脚本类型，这里使用的shell，默认是nodejs
- exec_mode:应用程序启动模式，这里设置的是cluster_mode（集群），默认是fork
- autorestart:启用/禁用应用程序崩溃或退出时自动重启
- vizion:启用/禁用vizion特性(版本控制)

可以通过`pm2 start processes.json`来启动。
也可以把命令写在package.json里。如下:

![img](https://upload-images.jianshu.io/upload_images/615807-241b23ec76dcda25.png?imageMogr2/auto-orient/strip%7CimageView2/2)

通过`npm run pm2`来启动。