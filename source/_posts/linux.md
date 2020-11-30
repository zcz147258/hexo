---
title: Linux
date:
updated:
type: "tags"
comments:
categories: Linux
description: Linux
keywords: Linux
top_img: https://ss0.bdstatic.com/70cFuHSh_Q1YnxGkpoWK1HF6hhy/it/u=1514243100,2352528106&fm=26&gp=0.jpg
cover: https://ss0.bdstatic.com/70cFuHSh_Q1YnxGkpoWK1HF6hhy/it/u=1514243100,2352528106&fm=26&gp=0.jpg
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
---
# 1.Nginx

```
专门为性能优化而开发。非常注重效率   支持高达5w个并发
支持热部署，启动特别容易，在不间断服务的情况下，可以对软件进行升级
yum install lrzsz
tar zxvf mongodb-linux.gz //解压

反向代理
	正向代理  局域网中的客户端访问internet，需要铜通过服务器代理
	反向代理  我们只需要将请求发送到反向代理服务器，反向代理服务器再去选择目标服务器获取数据，返回客户端，暴漏的是代理服务器地址，隐藏了真实的服务器地址
负载均衡
	把请求平均分发到多个服务器，实现负载均衡
动静分离
	为了加快网站的解析速度，把一些动态页面和静态页面，由不同的服务器来解析
	tomcat只放动态资源，jsp或者servlet，另外一个服务器放置静态资源
高可用

```

## 1.1安装运行

```xml
docker pull nginx

docker run -p 8080:80 -d docker.io/nginx 

linux上传文件
	xshell		安装 rz       yum   -y  install  lrzsz
	使用rz -y 命令进行上传

linux 查看开放的端口号  firewall-cmd --list-all
	  设置开放的端口号  firewall-cmd -add-serivce=http -permanent
	  				 sudo firewall-cmd --add-port=80/tcp -permanent
	  				 
	  重启防火墙       firewall-cmd --reload
nginx 常用操作命令
		/usr/local/nginx/sbin   进入
		
		查看版本号  ./nginx -v
		启动	./nginx
		关闭 ./nginx -s stop
		重新加载nginx   ./nginx -s reload


//非docker
tar -zxvf nginx-1.9.9.tar.gz
	//安依赖
	yum -y install gcc-c++
	yum -y install pcre-devel
	yum install -y zlib-devel
	//执行 ./configure
make install
//编辑配置
	vi /usr/local/nginx/conf/nginx.conf
//启动
	/usr/local/nginx/sbin/nginx -s reload
//启动不了 配置
	/usr/local/nginx/sbin/nginx -c /usr/local/nginx/conf/nginx.conf
//查询进程
	ps -ef | grep nginx
	查询nginx主进程号
　　ps -ef | grep nginx
　　从容停止   kill -QUIT 主进程号
　　快速停止   kill -TERM 主进程号
　　强制停止   kill -9 nginx
```

## 1.2nginx配置

```xml
进入  nginx容器  docker container exec -it 03c5eadf367d /bin/bash

cd /etc/nginx

查看文件  cat nginx.conf


	
配置文件由 三部分组成
	1.全局快
		影响nginx整体运行的【配置
		worker-proceses  1;  值越大  处理的并发数量越多
	2.events块
		影响nginx服务器和用户的网络连接
		 worker_connections  1024;  支持的最大连接数
	3.http块
		代理 缓存，和日志，高可用，反向代理，负载均衡等
		http块
			文件引入
			MIME——TYPE定义
			日志自定义
			连接超时时间
			单链接请求上限数量
		server块
			和虚拟主机由密切关系
				全局server
				location块
```

## 1.3反向代理

```xml
配置反向代理

		第一步
			在host文件中进行域名和ip对饮关系的配置
			192.168.212.54 www.123.com
		第二步
			    listen       80;
                server_name  47.101.212.62;

                #charset koi8-r;
                #access_log  /var/log/nginx/host.access.log  main;

                location / {
                    root   /usr/share/nginx/html;
                    proxy_pass  http://47.101.212.62:8081;
                    index  index.html index.htm;
                }
                
                
        多个服务器不同访问
        	加一个server
        	 listen : 9001
        	 server_name localhost;
        	 location ~ /edu/{
                 proxy_pass http://localhost:8001;
        	 }
        	 location ~ /vod/{
                 proxy_pass http://localhost:8001;
        	 }
```

## 1.4nginx详细配置

```xml
#user  nobody;
worker_processes  1; #工作进程：数目。根据硬件调整，通常等于cpu数量或者2倍cpu数量。
 
#错误日志存放路径
#error_log  logs/error.log;
#error_log  logs/error.log  notice;
#error_log  logs/error.log  info;
 
#pid        logs/nginx.pid; # nginx进程pid存放路径
 
 
events {
    worker_connections  1024; # 工作进程的最大连接数量
}
 
 
http {
    include       mime.types; #指定mime类型，由mime.type来定义
    default_type  application/octet-stream;
 
    # 日志格式设置
    #log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
    #                  '$status $body_bytes_sent "$http_referer" '
    #                  '"$http_user_agent" "$http_x_forwarded_for"';
 
    #access_log  logs/access.log  main; #用log_format指令设置日志格式后，需要用access_log来指定日志文件存放路径
                    
    sendfile        on; #指定nginx是否调用sendfile函数来输出文件，对于普通应用，必须设置on。
            如果用来进行下载等应用磁盘io重负载应用，可设着off，以平衡磁盘与网络io处理速度，降低系统uptime。
    #tcp_nopush     on; #此选项允许或禁止使用socket的TCP_CORK的选项，此选项仅在sendfile的时候使用
 
    #keepalive_timeout  0;  #keepalive超时时间
    keepalive_timeout  65;
 
    #gzip  on; #开启gzip压缩服务
 
    #虚拟主机
    server {
        listen       80;  #配置监听端口号
        server_name  localhost; #配置访问域名，域名可以有多个，用空格隔开
 
        #charset koi8-r; #字符集设置
 
        #access_log  logs/host.access.log  main;
 
        location / {
            root   html;
            index  index.html index.htm;
        }
        #错误跳转页
        #error_page  404              /404.html; 
 
        # redirect server error pages to the static page /50x.html
        #
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }
 
        # proxy the PHP scripts to Apache listening on 127.0.0.1:80
        #
        #location ~ \.php$ {
        #    proxy_pass   http://127.0.0.1;
        #}
 
        # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
        #
        #location ~ \.php$ { #请求的url过滤，正则匹配，~为区分大小写，~*为不区分大小写。
        #    root           html; #根目录
        #    fastcgi_pass   127.0.0.1:9000; #请求转向定义的服务器列表
        #    fastcgi_index  index.php; # 如果请求的Fastcgi_index URI是以 / 结束的, 该指令设置的文件会被附加到URI的后面并保存在变量$fastcig_script_name中
        #    fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;
        #    include        fastcgi_params;
        #}
 
        # deny access to .htaccess files, if Apache's document root
        # concurs with nginx's one
        #
        #location ~ /\.ht {
        #    deny  all;
        #}
    }
 
 
    # another virtual host using mix of IP-, name-, and port-based configuration
    #
    #server {
    #    listen       8000;
    #    listen       somename:8080;
    #    server_name  somename  alias  another.alias;
 
    #    location / {
    #        root   html;
    #        index  index.html index.htm;
    #    }
    #}
 
 
    # HTTPS server
    #
    #server {
    #    listen       443 ssl;  #监听端口
    #    server_name  localhost; #域名
 
    #    ssl_certificate      cert.pem; #证书位置
    #    ssl_certificate_key  cert.key; #私钥位置
 
    #    ssl_session_cache    shared:SSL:1m;
    #    ssl_session_timeout  5m; 
 
    #    ssl_ciphers  HIGH:!aNULL:!MD5; #密码加密方式
    #    ssl_prefer_server_ciphers  on; # ssl_prefer_server_ciphers  on; #
 
 
    #    location / {
    #        root   html;
    #        index  index.html index.htm;
    #    }
    #}
 
}
```



# 2.linux

```
1、开放端口
firewall-cmd --zone=public --add-port=5672/tcp --permanent   # 开放5672端口
firewall-cmd --zone=public --remove-port=5672/tcp --permanent  #关闭5672端口
firewall-cmd --reload   # 配置立即生效
systemctl start firewalld  //开启

2、查看防火墙所有开放的端口
firewall-cmd --zone=public --list-ports

3.、关闭防火墙
如果要开放的端口太多，嫌麻烦，可以关闭防火墙，安全性自行评估
systemctl stop firewalld.service

4.查看防火墙状态
firewall-cmd --state

5、查看监听的端口
netstat -lnpt

6、检查端口被哪个进程占用
netstat -lnpt |grep 5672

7、查看进程的详细信息
ps 6832

8、中止进程
kill -9 6832
```

## 2.1目录结构

```
管理类目录：
/dev 管理设备主要存放与设备有关的文件
/etc 主要存放系统配置方面的文件
/boot linux的内核及引导系统程序所需要的文件目录
/bin 存放标准 linux 的工具，在终端里输入ls，系统就系统将会到该目录查看是否存在该命令程序。
/sbin 大多是涉及系统管理的命令的存放，是超级权限用户root的可执行命令存放地
/var 用来存储经常被修改的文件，如日志、数据文件、邮箱等
/mnt 这个目录一般是用于存放挂载储存设备的挂载目录的

用户类目录：
/root 系统管理员目录
/home 家目录存放个人数据

应用程序类目录：
/lib 该目录用来存放系统动态链接共享库，几乎所有的应用程序都会用到该目录下的共享库
/tmp 临时目录，
/usr 存放一些不适合放在/bin 或 /etc 目录下的额外工具，如个人安装的程序或工具
/usr/local  主要存放那些手动安装的软件，
/usr/bin  用于存放程序
/usr/share  用于存放一些共享数据
/usr/lib  存放一些不能不能直接运行，但却是许多程序运行所必需的一些函数库文件
/opt   主要存放可选程序，直接删除程序不影响系统其设置。

信息类目录：
/lost+found 当系统意外崩溃或机器意外关机，而产生一些文件碎片放在这里。但当突然停电、或者非正常关机后，有些文件就临时存放在这里。
/proc 操作系统运行时，进程信息及内核信息（比如cpu、硬盘分区、内存信息等）存放在这里

```

## 2.2开关机操作

```
shutdown -h now 立即关机
shutdown -h 1 1分钟后关机
shutdown -r now 立即重启

sync 把内存的数据同步到磁盘中
```

## 2.3指令

```shell
pwd  显示当前工作目录的绝对路径
cd   切换目录
ls  列出文件列表
mkdir 创建目录
rmdir 删除目录
touch 创建空文件
cp  复制文件
rm  删除 rm -rf 递归删除
mv 移动文件夹
cat 查看文件内容 -n 显示行号
cat -n /etc/profile | more  分页显示
more 查看文件分页  enter一行一行前进
less 更加强大 效率高  和more类似
> 输出重定向 会将原来的文件覆盖 ls -l > a.txt
>>  追加  不会覆盖原来的文件追加到尾部 
head -n 5  默认查看前10行   查看文件前5行

ln  软链接 快捷方式  ln -s /root LinkToRoot
history  可以查看执行的历史指令 也可以执行历史指令  history 10  展示最近10个  !5 执行编号5指令


date 显示当前时间  date+%Y  展示年份
cal 查看日历


搜索查找类
find 查询 find / -size +20M  查询大于20M
| 表示 将前一个命令的输出结果传递给后一个命令处理 cat hello.txt | grep -n yes
```



# 3.Docker

```
是一个开源的应用容器引擎，类似于虚拟机技术，不是一个虚拟机，基于 GO语言
支持将一个软件编译成为一个镜像，然后再镜像中各种软件做好配置，将镜像发布出去，其他使用者可以直接使用这个镜像

```

## 3.1核心概念

```java
docker主机：安装了docker程序的机器。
docker客户端： 连接docker主机进行操作。
docker仓库  用来保存各种软件镜像的地方   dockerhub是docker的公共仓库
docker镜像  docker仓库里面放着docker镜像
docker容器： 运行镜像产生容器

使用docker
		1.安装docker
		2.去docker仓库找这个软件对应的镜像
		3.使用docker运行这个镜像，生成一个docker容器
		4.对容器的启动停止就是对软件的启动停止
		
		查看linux的 ip地址   ip addr
docker  里面拷贝文件
	1.从容器拷贝文件到宿主机
		docker cp 03c5eadf367d:/etc/nginx/nginx.conf /usr/conf/
	2.从宿主机拷贝文件到容器
		docker cp /opt/test/file.txt mycontainer:/opt/testnew/
```

## 3.2安装docker

```java
 更新		 sudo yum update
 安装软件包  sudo yum install -y yum-utils device-mapper-persistent-data lvm2
 设置    yum  源  
  sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
  
  
 uname -r  检查内核
 yum install docker  安装docker
 输入 y   安装
 启动docker  systemctl start docker
检查 版本    docker -v
开机启动docker  systemctl enable docker

dockers中安装  vim
mv /etc/apt/sources.list /etc/apt/sources.list.bak
    echo "deb http://mirrors.163.com/debian/ jessie main non-free contrib" >/etc/apt/sources.list
    echo "deb http://mirrors.163.com/debian/ jessie-proposed-updates main non-free contrib" >>/etc/apt/sources.list
    echo "deb-src http://mirrors.163.com/debian/ jessie main non-free contrib" >>/etc/apt/sources.list
    echo "deb-src http://mirrors.163.com/debian/ jessie-proposed-updates main non-free contrib" >>/etc/apt/sources.list
    #更新安装源
    apt-get update   更新资源
		apt-get install vim
		
docker文件挂载同步操作
	docker run -p 80:80 -v /data:/data -d nginx:latest
	使用镜像 nginx:latest，以后台模式启动一个容器,将容器的 80 端口映射到主机的 80 端口,主机的目录 /data 映射到容器的 /data。
	 冒号:前面是宿主机的文件夹地址，冒号:后面是docker容器中的文件夹地址。
	挂载tomcat  docker run -p 8081:80 -v /data/tomcat1:/webapps -d tomcat
```

## 3.3常用搜索

```java
docker search mysql   搜索，检索
docker pull 镜像名 ：tag   表示版本 不加就是最新的版本
docker images   查看所有镜像
docker rmi image-id    删除指定的本地镜像

查看linux  内核版本
lsb_release -a


解决centos网关 

方法一、

　　1、打开 vi /etc/sysconfig/network-scripts/ifcfg-eth0（每个机子都可能不一样，但格式会是“ifcfg-eth数字”），把ONBOOT=no，改为ONBOOT=yes

　　2、重启网络：service network restart

方法二、

　　1、打开 vi /etc/resolv.conf，增加 nameserver 8.8.8.8

　　2、重启网络: service network restart
三
	vi /etc/sysconfig/network-scripts/ifcfg-eth0
	追加 
		DNS1=8.8.8.8
		DNS2=4.2.2.2
添加  DNS解析 
	在etc/reslove.conf添加个公共dns解析试试（114.114.114.114或者8.8.8.8）
	参考第三条，https://support.huaweicloud.com/dns_faq/dns_faq_003.html

	容器操作
	docker启动命令,docker重启命令,docker关闭命令

启动        systemctl start docker
守护进程重启   sudo systemctl daemon-reload
重启docker服务   systemctl restart  docker
重启docker服务  sudo service docker restart
关闭docker service docker stop
关闭docker systemctl stop docker
	
	根据镜像启动容器
	1.运行  docker run --name diyname -d redis  
		diyname 自定义容器名   -d 后台运行  redis 镜像名称  
	2.查看列表中容器
		docker ps   查看运行中的容器   查询所有的容器  docker ps -a
	3.停止运行中的容器
		docker stop name/id
	4.删除指定容器
		docker rm container -id
	5.端口映射
		docker run  -d -p 6397:6397 --name diynameredis   主机映射到容器内部的端口
		docker run -d -p 8080:8080 tomcat
		
		docker exec -it ddd99f5b7948 /bin/bash 进入tomcat容器下面
		cp -r /usr/local/tomcat/webapps.dist/* /usr/local/tomcat/webapps/
		复制  wabapps.dist  到  webapps目录下面
		//开启mysql连接映射
		docker run --name mysqltest -p 3389:3306 -e MYSQL_ROOT_PASSWORD=123456 -d mysql
	6.防火墙
		service firewalld status   查看防火墙
		service firewalld stop 停止防火
	7.容器日志
		docker logs container-name/container-id
		
	8.进入容器内部
		有个命令，可以进入容器内部,ctrl+p+q可以以后台运行的方式退出这个软件
		docker exec -it 容器的id /bin/bash
		docker exec -it bcc21907ed58 /bin/bash
 		mysql -uroot -p123456
 		
 		ALTER USER 'root'@'localhost' IDENTIFIED BY '你的密码' PASSWORD EXPIRE NEVER; # 修改加密规则 
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '你的密码'; # 更新一下用户的密码 
FLUSH PRIVILEGES; #刷新权限
```

## 3.4搭建项目环境

```java
安装  ftp  yum install -y lrzsz
zip解压  
安装命令： yum install zip    #提示输入时，请输入y；
安装命令：yum install unzip #提示输入时，请输入y；
一...配置java环境

1.安装 centos并且 挂载到本地目录上
docker run -i -t -v /root/software/:/mnt/software/ --privileged=true 470671670cac

2.安装vim编辑器
	apt-get update   更新资源
		apt-get install vim
	
3.解压jdk  tar -xvf jdk-8u11-linux-x64.tar.gz 
4.设置环境变量
	vim /etc/profile
	/root/software/java/jdk1.8.0_11
	文本得末尾追加
		JAVA_HOME=/usr/jdk
		CLASSPATH=$JAVA_HOME/lib/
		PATH=$PATH:$JAVA_HOME/bin
		export PATH JAVA_HOME CLASSPATH
5.保存文件退出
	建立一个短链接节省长度
	ln -s /root/software/java/jdk1.8.0_11 /usr/jdk
	:wq
6.重启机器
7.配置java环境成功

二.配置tomcat环境
docker run -d -p 8080:8080 tomcat
	1.<packaging>war</packaging>  就可以将打包为  war包
	2.上传文件到宿主机  然后复制到 容器内部
		docker cp servey-0.0.1-SNAPSHOT.war 6d1bba76a9cf:/usr/local/tomcat/webapps
	3.修改文件名称
		mv /usr/bin/python_old /usr/bin/python_new
	4.打war包注意
@SpringBootApplication
public class ServeyApplication extends SpringBootServletInitializer{
//    @Override
//    protected SpringApplicationBuilder configure(SpringApplicationBuilder builder) {
//        return super.configure(builder);
//    }

    public static void main(String[] args) {
        SpringApplication.run(ServeyApplication.class, args);
    }

}
	centos
	加速
		sudo yum update
	//开放端口
	1、开启防火墙 
    	systemctl start firewalld
		查看防火墙状态
		停止firewall
		禁止firewall开机启动
		systemctl disable firewalld.service 
		systemctl stop firewalld.service
		firewall-cmd --state
	2、开放指定端口
     	 firewall-cmd --zone=public --add-port=1935/tcp --permanent
     	 firewall-cmd --permanent --add-port=8080/tcp
 	命令含义：
		--zone #作用域
		--add-port=1935/tcp  #添加端口，格式为：端口/通讯协议
		--permanent  #永久生效，没有此参数重启后失效

	3、重启防火墙
      	firewall-cmd --reload

	4、查看端口号
		netstat -ntlp   //查看当前所有tcp端口·
		netstat -ntulp |grep 1935   //查看所有1935端口使用情况·
	ubuntu
		安装
			$ sudo apt-get update
			$ sudo apt-get install iptables
		开发端口
			$ sudo iptables -I INPUT -p tcp --dport 8000 -j ACCEPT
		保存规则
			$ iptables-save 
		永久保存
			$ sudo apt-get install iptables-persistent
			
			http://47.101.212.62:8080/servey/all
三.配置数据库环境
	1.运行mysql
	docker run -p 3307:3306 --name mysql -e MYSQL_ROOT_PASSWORD=123456 -d mysql:5.7
	2.进入数据库 不然远程会连接不上
		输入密码
	3.运行sql文件
四.永久后台运行
	nohup java -jar servey-0.0.1-SNAPSHOT.jar >/opt/project/really/servey-0.0.1-SNAPSHOT.out 2>&1 &
java -jar /web/share-book.jar > /web/log.txt &   jar包日志
	ps  查看当前得所有进程  -a 显示所有程序
	&   把这个命令放在后台执行
	nohub  不间断得运行命令
	停止运行项目
		1.ps -ef
		2.kill 
		
		
		后台运行
		$ nohup java -jar test.jar &
 
//nohup 意思是不挂断运行命令,当账户退出或终端关闭时,程序仍然运行
//当用 nohup 命令执行作业时，缺省情况下该作业的所有输出被重定向到nohup.out的文件中
//除非另外指定了输出文件。

$ nohup java -jar test.jar >temp.txt &
 
//这种方法会把日志文件输入到你指定的文件中，没有则会自动创建


设置tomcat默认访问路劲
	<Context path="" docBase=""  reloadable="true"/>
```

# 4.mysql无法启动

```java
百度后得知是因为虚拟内存不够无法启动mysql

于是查询服务器 虚拟内存 

free

发现swap 虚拟内存都是0

应该是swap 未启用

启用swap:

dd if=/dev/zero of=/swapfile bs=1M count=1024
   
mkswap /swapfile

swapon /swapfile

再次 free

发现swap 已经有数值 已启用

再次 docker start mysql

启动成功  
————————————————
版权声明：本文为CSDN博主「white_bird_shit」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/white_bird_shit/article/details/87343187
```

# 5.vim

```
 1) 命令行模式command mode）
　　控制屏幕光标的移动，字符、字或行的删除，移动复制某区段及进入Insert mode下，或者到 last line mode。
 2) 插入模式（Insert mode）
　只有在Insert mode下，才可以做文字输入，按「ESC」键可回到命令行模式。
　在「命令行模式（command mode）」下按一下字母「i」就可以进入「插入模式（Insert mode）」，这时候你就可以开始输入文字了。
 3) 底行模式（last line mode）
　将文件保存或退出vi，也可以设置编辑环境，如寻找字符串、列出行号……等。
　

```

## 5.1命令

```

vi myfile   是处于「命令行模式（command mode）
: w filename （输入 「w filename」将文章以指定的文件名filename保存）
: wq (输入「wq」，存盘并退出vi)
: q! (输入q!， 不存盘强制退出vi)

:set number  设置行号

```

# 6.安装Mongodb

```shell
tar zxvf mongodb-linux.gz

创建配置文件  
	重命名
		mv mongodb mongodbserver
	创建数据库文件夹
		mkdir data  
		或者  db
	创建日志文件夹
		mkdir log
	创建配置文件夹etc
		mkdir etc
		创建配置文件mongodb.conf
		vim mongodb.conf
			th=/usr/local/databse/mongodb/db
            logpath=/usr/local/database/mongodb/log/mongodb.log
            port=27017
            fork=true
            journal=false
            storageEngine=mmapv1
		
		
//启动MongoDB
	./mongod --dbpath=/root/database/mongodbserver/db
	./mongod --config /root/database/mongodbserver/etc/mongodb.conf
//正确关闭数据库
	use admin
	db.shutdownServer()
//看到 
	http://47.101.212.62:27017/  
	成功  
//It looks like you are trying to access MongoDB over HTTP on the native driver port.

//将mongod路径添加到系统路径中，方便随处执行mongod命令
1. 在/etc/profile文件中，添加
	export PATH=$PATH:/root/database/mongodbserver/bin
2.执行source /etc/profile，使系统环境变量立即生效
3.将mongo路径软链到/usr/bin路径下，方便随处执行mongo命令
 ln -s /root/database/mongodbserver/bin/mongo  /usr/bin/mongo
 
 
 //配置权限
 //创建超级管理员账户
    db.createUser({
        user:'admin',
        pwd:'123456',
        roles:[{role:'root',db:'admin'}]
    })
    db.createUser({user:"adminroot",pwd:"123456",roles:[{
    role:"root",db:"admin"
    }]})
    //第二步修改配置文件
    配置
    security:
      authorization: enabled
    //第三步
    //首先创建用户管理员
    db.createUser(
      {
        user: "admin",
        pwd: "123456",
        roles: [ { role: "userAdminAnyDatabase", db: "admin" } ]
      }
    )
    //管理员登录
    mongo admin -u admin -p"123456"
    //创建普通用户
    	use admin
        db.createUser(
        {user:'user',
         pwd:'passwd', 
         roles:[
           {role:'readWrite', db:'userdb'}
        ]
        })

        db.createUser(
        {user:'user1',
         pwd:'passwd1', 
         roles:[
           {role:'root', db:'userdb'}
        ]
        })
    //关闭数据库
    kill -9 pid
    
    
    
    //非正常关闭删除  db文件下面的  mongod.lock
```

# 7.部署node

```
xz -d node-v12.18.3-linux-x64.tar.xz  解压压缩包
./node -v 检查版本
./npm -v   npm版本

//软连接  简单配置
	ln -s /root/server/node/nodejs/bin/node /usr/local/bin/node
	ln -s /root/server/node/nodejs/bin/npm /usr/local/bin/npm、
//环境变量
	vi /etc/profile
	export PATH=$PATH:/root/server/node/nodejs/bin
	source /etc/profile
//yum install -y unzip zip
/npm install -g cnpm --registry=https://registry.npm.taobao.org

//supervisor bin/www
//后台运行
nohup node servier.js &
```

# 8.React项目部署nginx

```
  pages.json
 	 "homepage":".",
  nginx
	 location /adminback {
            root   /root/;
           try_files $uri $uri/ /index.html;
      }
```

# 9.部署SSR项目

## 9.1next.js

```
npm run build
npm run start
build完成的内容会生成到.next文件夹内，npm run start之后，我们访问的实际上就是.next文件夹的内容。

运行多个实例
如果我们需要进行横向扩展（ Horizontal Scale）以提高网站的访问速度，我们需要运行多个网站的实例。首先，我们修改package.json的start script：
	"start": "next start -p $PORT"
	如果是windows系统：
	"start": "next start -p %PORT%"
	PORT=8000 npm start
	PORT=9000 npm start	
```

