title: 单节点Nginx环境搭建
tags: [nginx]
keyword: nginx,nginx环境搭建
categories: nginx
date: 2017-04-16 23:46

---

　　上星期，由于工作需要，要搭建一个nginx服务器用于公司业务系统的反向代理，大概了解了一下，就动手搭建了一下，顺便出一个教程，方便新(zi)手(ji)查阅<!-- more -->
#### 一、安装Nginx
1. 点击[这里](https://nginx.org/en/download.html)，下载安装最新版本Nginx,并解压安装包：` tar -zxvf nginx-xxxx.tar.gz `
2. 安装Nginx编译必须的lib包，pcre、zlib和OpenSSL：
	` yum -y install pcre-devel ` 
	` yum install openssl openssl-devel `
	` yum install -y zlib-devel `
3. 检查Nginx必须的lib是否已经有了：` ./configure --with-http_ssl_module `，若出现以下内容则表示lib已经安装
![xx](http://i1.piimg.com/591560/4716d3856ba6e9f4.png)
4. 定位到nginx目录，运行` make `命令进行编译，然后切换到root权限，到nginx目录执行` make install `命令进行安装
5. 定位到安装路径下：` /usr/local/nginx/sbin `，运行命令` ./nginx `，在浏览器中输入阿里云的host地址，如果出现下图类似内容，则安装成功
![xx](http://i1.piimg.com/591560/af24b8e898055aed.png)

### 二、配置nginx配置文件
1. 将证书和key放在*/usr/local/nginx/conf*目录下，下面备用
2. 打开并下载路径*/usr/local/nginx/conf*下的***nginx.conf***文件：
　　1. 将***worker_processes***(允许生成的进程数)、***worker_connections ***(最大连接数)设置大点
　　2. 配置代理服务器，在此均使用单节点的方式进行:
		```xml
		upstream myappServer{
			server localhost:8001;
		}```
以此类推，配置多个系统
　　3. 配置server模块：
        ```xml
		client_max_body_size 500M;   --上传文件限制大小
		listen       80 default backlog=2048; --监听端口
		listen 443 ssl; --ssl加密传输接口
		server_name  localhost; 
		ssl_certificate      /usr/local/nginx/conf/server.crt; --ssl证书
		ssl_certificate_key  /usr/local/nginx/conf/server.key; --ssl key

		proxy_set_header       Host $host;  --主域名
		proxy_set_header  X-Real-IP  $remote_addr; --真实地址
		proxy_set_header  X-Forwarded-For $proxy_add_x_forwarded_for;
		proxy_set_header X-Forwarded-Proto  $scheme;```

	4. 匹配规则：
		```xml
		location /myapp/ {   --匹配规则为*/mychs/*的地址请求
			proxy_pass http://mychsServer/myapp/; -- mychsServer对应上面的myServer
		}```
3. 保存，定位到***sbin***目录下,运行命令`./nginx -s reload `即可重新加载nginx配置文件


### 常用命令：
启动 Nginx：` sudo ./sbin/nginx `
停止 Nginx：` sudo ./sbin/nginx -s stop `或` sudo ./sbin/nginx -s quit`
Nginx 重载配置: ` sudo ./sbin/nginx -s reload `
查看配置文件是否正确: ` ./sbin/nginx –t`
强制停止: ` pkill -9 nginx `

	
	