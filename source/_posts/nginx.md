---
title: nginx
date: 2022-05-07 14:05:34
tags: [nginx]
---

<meta name="referrer" content="no-referrer"/>

# Nginx简介

## 什么是nginx

- Nginx 是**高性能的 HTTP 和反向代理的服务器**，处理高并发能力是十分强大的，能经受高负载的考验,有报告表明能支持高达 50,000 个并发连接数。

- Nginx (engine x) 是一个高性能的HTTP和反向代理web服务器，同时也提供了
  IMAP/POP3/SMTP服务。Nginx是由伊戈尔·赛索耶夫为俄罗斯访问量第二的
  Rambler.ru站点（俄文：Рамблер）开发的，第一个公开版本0.1.0发布于2004
  年10月4日。
- 其将源代码以类BSD许可证的形式发布，因它的稳定性、丰富的功能集、简单的配
  置文件和低系统资源的消耗而闻名。2011年6月1日，nginx 1.0.4发布。
  Nginx是一款轻量级的Web 服务器/反向代理服务器及电子邮件（IMAP/POP3）
  代理服务器，在BSD-like 协议下发行。其特点是占有内存少，并发能力强，事实
  上nginx的并发能力在同类型的网页服务器中表现较好，中国大陆使用nginx网站
  用户有：百度、京东、新浪、网易、腾讯、淘宝等。

## 正向代理

- 需要**在客户端配置代理服务器**进行指定网站访问

  ![image-20220912114511292](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220912114511292.png)

## 反向代理

- 对外暴露的是代理服务器的地址，隐藏了真实服务器的IP地址，需要**在服务端配置反向代理服务器**。

  ![image-20220912114641575](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220912114641575.png)

## 负载均衡

- 增加服务器的数量，然后将请求分发到各个服务器上，将原先请求集中到单个服务器上的
  情况改为将请求分发到多个服务器上，将负载分发到不同的服务器，也就是我们所说的负
  载均衡，也就是说**将发过来的请求按照设定的模式分发到各个服务器上**。

  ![image-20220912114755582](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220912114755582.png)

## 动静分离

- 将动态资源和静态资源分别放到不同的地方提供访问。

  ![image-20220912114847888](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220912114847888.png)

# Nginx的安装

- 由于在windows操作系统上安装Nginx非常简单，在这里也就不再赘述，主要是走一遍在Linux系统上安装Nginx的流程。

## 准备工作

1. 打开Linux操作系统

2. 到nginx官网下载软件[官网](http://nginx.org/)

   ![image-20220912115353859](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220912115353859.png)

## 开始进行nginx安装

### 安装pcre依赖

1. 联网下载 pcre 压缩文件依赖：**wget http://downloads.sourceforge.net/project/pcre/pcre/8.37/pcre-8.37.tar.gz**

   ![image-20220912115538865](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220912115538865.png)

2. 解压压缩文件，使用命令：**tar –xvf pcre-8.37.tar.gz**

3. ./configure 完成后，回到 pcre 目录下执行 make，最后执行 make install

   ![image-20220912115719998](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220912115719998.png)

### 安装openssl、zlib、gcc依赖

1. 使用命令：**yum -y install make zlib zlib-devel gcc-c++ libtool openssl openssl-devel**

## 安装nginx

1. 使用命令**tar –xvf 文件名**解压
2. 使用命令**./configure**
3. 使用**make和make install**命令进行安装

## 启动服务

1. 进入目录 /usr/local/nginx/sbin/nginx 启动服务


## 防火墙问题

- 在 windows 系统中访问 linux 中 nginx（虚拟机），默认不能访问的，因为防火墙问题，所以要关闭防火墙、开放80端口的访问权限。
- 查看开放的端口号：**firewall-cmd --list-all**
- 设置开放的端口号：**firewall-cmd --add-service=http –permanent**、**firewall-cmd --add-port=80/tcp --permanent**
- 重启防火墙：**firewall-cmd –reload**

![image-20220912205349826](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220912205349826.png)

# Nginx的常用命令（Linux）

- 首先要进入到nginx目录下

## 查看nginx版本号

- **./nginx -v**

  ![image-20220912205657380](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220912205657380.png)

## 启动nginx

- **./nginx**

## 停止nginx

- **./nginx -s stop**

## 重新加载nginx

- **./nginx -s reload**

# Nginx的配置文件

## Nginx配置文件的位置

- **nginx/conf/nginx.conf**

  ![image-20220912205908806](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220912205908806.png)

## 配置文件中的内容

- 包含三部分内容：
  1. **全局块**：配置服务器整体运行的配置指令，比如 worker_processes 1;用于处理并发数的配置。
  2. **events块**：影响 Nginx 服务器与用户的网络连接比如 worker_connections 1024; 表示支持的最大连接数为 1024
  3. **http块**：其中还包含两部分：**http 全局块和server 块**

## 配置location块

- Location 块通过指定模式来与客户端请求的URI相匹配。Location基本语法：

  1. 匹配 URI 类型，有四种参数可选，当然也可以不带参数。

  2. 命名location，用@来标识，类似于定义goto语句块。

     ![image-20220912213437953](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220912213437953.png)

## location匹配命令解释

![image-20220912213500423](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220912213500423.png)

# Nginx配置实例-反向代理实例1

## 要实现的效果

- 打开浏览器，在浏览器地址栏输入地址www.baidu.com，跳转到 liunx 系统 tomcat 主页
  面中

## 准备工作

1. 在 liunx 系统安装 tomcat，使用默认端口 8080： tomcat 安装文件放到 liunx 系统中，解压，进入 tomcat 的 bin 目录中，./startup.sh 启动 tomcat 服务器

2. 对外开放访问的端口：**firewall-cmd --add-port=8080/tcp --permanent**、**firewall-cmd –reload**，查看已经开放的端口号：**firewall-cmd --list-all**

3. 在windows系统中通过浏览器访问tomcat服务器

   ![image-20220912210730416](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220912210730416.png)

## 访问过程的分析

![image-20220912210806958](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220912210806958.png)

## 具体配置

1. 在windows系统的host文件中进行域名和ip对应关系的配置，在hosts文件中的最后添加一组IP映射：**nginx所在服务器的ip 代理网站域名**

   ![image-20220912210926234](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220912210926234.png)

2. 在nginx进行请求转发的配置（反向代理配置）

   ![image-20220912211346377](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220912211346377.png)

## 最终测试

![image-20220912211509007](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220912211509007.png)

# Nginx配置实例-反向代理实例2

## 要实现的效果

- 使用 nginx 反向代理，根据访问的路径跳转到不同端口的服务中，nginx的监听端口为9001，比如：访问 http://192.168.17.129:9001/edu/ 直接跳转到 127.0.0.1:8080，访问 http://192.168.17.129:9001/vod/ 直接跳转到 127.0.0.1:8081

## 准备工作

1. 准备两个tomcat服务器，一个端口号是8080，一个端口号是8081
2. 创建文件夹和测试页面

## 具体配置

1. 找到nginx配置文件，进行反向代理配置

   ![image-20220912211921300](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220912211921300.png)

2. 开放对外访问的端口号：9001、8080、8081

## 最终测试

![image-20220912213610650](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220912213610650.png)

# Nginx配置实例-负载均衡

## 要实现的效果

- 浏览器地址栏输入地址 http://192.168.17.129/edu/a.html，负载均衡效果，将请求平均分布到 8080和 8081端口中

## 准备工作

1. 准备两台 tomcat 服务器，一台开 8080端口，一台开 8081端口

2. 在两台 tomcat 里面 webapps 目录中，创建名称是 edu 文件夹，在 edu 文件夹中创建页面 a.html，用于测试

3. 在 nginx 的配置文件中进行负载均衡的配置：

   ![image-20220912214038708](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220912214038708.png)

## Nginx分配服务器的策略

1. 轮询（默认），每个请求按时间顺序逐一分配到不同的后端服务器，如果后端服务器 down 掉，能自动剔除。
2. weight，weight 代表权重默认为 1,权重越高被分配的客户端越多
3. ip_hash，每个请求按访问 ip 的 hash 结果分配，这样每个访客固定访问一个后端服务器
4. fair（第三方），按后端服务器的响应时间来分配请求，响应时间短的优先分配。

# Nginx配置实例-动静分离

## 什么是动静分离

![image-20220912214303161](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220912214303161.png)

- 通过 location 指定不同的后缀名实现不同的请求转发。通过 expires 参数设置，可以使浏
  览器缓存过期时间，减少与服务器之前的请求和流量。具体 Expires 定义：是给一个资源
  设定一个过期时间，也就是说无需去服务端验证，直接通过浏览器自身确认是否过期即可，所以不会产生额外的流量。此种方法非常适合不经常变动的资源。（如果经常更新的文件，不建议使用 Expires 来缓存），我这里设置 3d，表示在这 3 天之内访问这个 URL，发送一个请求，比对服务器该文件最后更新时间没有变化，则不会从服务器抓取，返回状态码 304，如果有修改，则直接从服务器重新下载，返回状态码 200。

## 准备工作

1. 在linux系统中准备静态资源，用于进行访问：

   ![image-20220912214436989](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220912214436989.png)

## 具体配置

1. 在 nginx 配置文件中进行配置

   ![image-20220912214655466](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220912214655466.png)

## 最终测试

1. 在浏览器中输入地址：http://192.168.17.129/image/01.jpg

   ![image-20220912214823527](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220912214823527.png)

2. 配置了**autoindex on**后可以看到一层下的所有静态文件：

   ![image-20220912214924668](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220912214924668.png)

3. 在浏览器输入地址：http://192.168.17.129/www/a.html

   ![image-20220912215010083](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220912215010083.png)

# Nginx配置高可用的集群

## 什么是nginx高可用

![image-20220912215045661](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220912215045661.png)

- 需要两台nginx服务器
- 需要keepalived
- 需要虚拟ip

## 配置高可用的准备工作

1. 需要两台服务器 192.168.17.129 和 192.168.17.131
2. 在两台服务器安装 nginx
3. 在两台服务器安装 keepalived

## 在两台服务器安装keepalived

1. 使用yum命令进行安装：**yum install keepalived –y**
2. 安装之后，在 etc 里面生成目录 keepalived，有文件 keepalived.conf

## 完成高可用配置（主从配置）

1. 修改/etc/keepalived/keepalivec.conf 配置文件

   ```
   global_defs {
   	notification_email {
   		acassen@firewall.loc
   		failover@firewall.loc
   		sysadmin@firewall.loc
   	}
   	notification_email_from Alexandre.Cassen@firewall.loc
   	smtp_server 192.168.17.129
   	smtp_connect_timeout 30
   	router_id LVS_DEVEL
   }
   vrrp_script chk_http_port {
   	script "/usr/local/src/nginx_check.sh"
   	interval 2 #（检测脚本执行的间隔）
   	weight 2
   }
   vrrp_instance VI_1 {
   	state BACKUP # 备份服务器上将 MASTER 改为 BACKUP
   	interface ens33 //网卡
   	virtual_router_id 51 # 主、备机的 virtual_router_id 必须相同
   	priority 90 # 主、备机取不同的优先级，主机值较大，备份机值较小
   	advert_int 1
   	authentication {
   		auth_type PASS
   		auth_pass 1111
   	}
   	virtual_ipaddress {
   		192.168.17.50 // VRRP H 虚拟地址
   	}
   }
   ```

2. 在/usr/local/src 添加检测脚本

   ```shell
   #!/bin/bash
   A=`ps -C nginx –no-header |wc -l`
   if [ $A -eq 0 ];then
   	/usr/local/nginx/sbin/nginx
   	sleep 2
   	if [ `ps -C nginx --no-header |wc -l` -eq 0 ];then
   		killall keepalived
   	fi
   fi
   ```

   3. 把两台服务器上 nginx 和 keepalived 启动、启动 nginx：./nginx、启动 keepalived：systemctl start keepalived.service

## 最终测试

1. 在浏览器地址栏输入 虚拟 ip 地址 192.168.17.50

   ![image-20220912215836587](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220912215836587.png)

![image-20220912215851619](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220912215851619.png)

2. 把主服务器（192.168.17.129）nginx 和 keepalived 停止，再输入 192.168.17.50

   ![image-20220912215911674](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220912215911674.png)

# Nginx的原理

## master 和 worker

![image-20220912215944477](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220912215944477.png)

## worker是如何进行工作的

![image-20220912220007824](https://konjacer-blog-img-repo.oss-cn-qingdao.aliyuncs.com/img/image-20220912220007824.png)

## 一个master和多个worker的好处

1. 可以使用 nginx –s reload 热部署，利用 nginx 进行热部署操作
2. 每个 woker 是独立的进程，如果有其中的一个 woker 出现问题，其他 woker 独立的，继续进行争抢，实现请求过程，不会造成服务中断

## 设置多少个worker合适

- worker 数和服务器的 cpu 数相等是最为适宜的

## 关于连接数 worker_connection的问题

1. 发送请求，占用了 woker 的几个连接数？答案：2或者4，可以直接处理，或者转发到tomcat处理请求，每次处理都要开来回两个连接数
2. nginx 有一个 master，有四个 woker，每个 woker 支持最大的连接数 1024，支持的最大并发数是多少？
   - 普通的静态访问最大并发数是： worker_connections * worker_processes / 2，
   - 而如果是 HTTP 作 为反向代理来说，最大并发数量应该是 worker_connections *
     worker_processes / 4。

# nginx常见问题

## 在nginx上部署了静态页面，访问的时候却说拒绝访问

- **nginx路径下不能存在中文**。
