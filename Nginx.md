## Nginx

> **Nginx**（发音同“engine X”）是异步框架的[网页服务器](https://zh.wikipedia.org/wiki/網頁伺服器)，也可以用作[反向代理](https://zh.wikipedia.org/wiki/反向代理)、[负载平衡器](https://zh.wikipedia.org/wiki/负载均衡)和[HTTP缓存](https://zh.wikipedia.org/wiki/HTTP缓存)。
>
> 特点：占用内存少，并发力强
---
#### 反向代理

> 正向代理【用户---》代理服务器----》google.com】
>
> 反向代理，其实客户端对代理是无感知的，因为客户端不需要任何配置就可以访问，我们只需要将请求发送到反向代理服务器，由反向代理服务器去选择目标服务器获取数据后，在返回给客户端，此时反向代理服务器和目标服务器对外就是一个服务器，暴露的是代理服务器地址，隐藏了真实服务器IP地址。

#### 负载均衡

>将大量请求进行分布式处理的策略。

1. 轮询：
2. **加权轮询**
3. **IP 哈希（IP hash）**
4. URL hash

####  动静分离

#### 常用指令

```shell
wget http://nginx.org/download/nginx-1.14.2.tar.gz
# 安装依赖
yum -y install gcc zlib zlib-devel pcre-devel openssl openssl-devel
# 解压缩
tar -zxvf linux-nginx-1.14.2.tar.gz
cd nginx-1.14.2/
# 执行配置
./configure	
# 相对应的木块
./configure	 --prefix=/root/sdSoft/nginx --with-http_ssl_module --with-http_gzip_static_module --with-http_stub_status_module --with-http_slice_module --with-http_v2_module --with-stream_ssl_module
# 编译安装(默认安装在/usr/local/nginx)
make & make install

```

#### 模块添加

```shell
#查看已安装的模块
nginx -V 
(1)解压同版本源码
(2)cd 到解压目录
--prefix=/data/soft/nginx1.14.2 --with-http_ssl_module --with-http_gzip_static_module --with-http_stub_status_module --with-http_slice_module --with-http_v2_module --with-stream_ssl_module
make
```



####  环境变量配置

```shell
export NGINX_HOME=/usr/local/nginx
export PATH=$PATH:$NGINX_HOME/sbin
```



```shell

yum -y install --install root=/usr/local nginx   # 安装 nginx到指定目录
yum remove nginx  # 卸载 nginx
systemctl enable nginx # 设置开机启动 
nginx -c /etc/nginx/nginx.conf #启动 nginx 服务
nginx -s stop # 停止 nginx 服务
nginx restart # 重启 nginx 服务
nginx -s reload # 重新加载配置，一般是在修改过 nginx 配置文件时使用。
nginx -t       # 测试配置文件是否正确

systemctl start nginx.service　（启动nginx服务）
systemctl stop nginx.service　（停止nginx服务）
systemctl enable nginx.service （设置开机自启动）
systemctl disable nginx.service （停止开机自启动）
systemctl status nginx.service （查看服务当前状态）
systemctl restart nginx.service　（重新启动服务）
systemctl list-units --type=service （查看所有已启动的服务）
```

#### 配置自启

##### 方式一

(1) vim /lib/systemd/system/nginx.service

记得修改目录名称

```shell
[Unit]
Description=nginx
After=network.target
 
[Service]
Type=forking
ExecStart=/usr/local/nginx/sbin/nginx
ExecReload=/usr/local/nginx/sbin/nginx -s reload
ExecStop=/usr/local/nginx/sbin/nginx -s quit
PrivateTmp=true

[Install]
WantedBy=multi-user.target


Description:描述服务
After:描述服务类别
[Service]服务运行参数的设置
Type=forking是后台运行的形式
ExecStart为服务的具体运行命令
ExecReload为重启命令
ExecStop为停止命令
PrivateTmp=True表示给服务分配独立的临时空间
注意：[Service]的启动、重启、停止命令全部要求使用绝对路径
[Install]运行级别下服务安装的相关设置，可设置为多用户，即系统运行级别为3

保存退出。
# 设置服务生效
systemctl daemon-reload
```



（3）systemctl enable nginx.service

##### 方式二

```shell
vim /etc/rc.local

添加
/usr/local/nginx/sbin/nginx
```



#### 配置文件

(1)全局块

(2)event

(3)http块

```shell
user nginx;
worker_processes auto; #处理的并发量
error_log /var/log/nginx/error.log;
pid /run/nginx.pid;

# Load dynamic modules. See /usr/share/doc/nginx/README.dynamic.
include /usr/share/nginx/modules/*.conf;

events {
    worker_connections 1024; #最大的连接数
}

http {
    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /var/log/nginx/access.log  main;

    sendfile            on;
    tcp_nopush          on;
    tcp_nodelay         on;
    keepalive_timeout   65;
    types_hash_max_size 2048;

    include             /etc/nginx/mime.types;
    default_type        application/octet-stream;

    # Load modular configuration files from the /etc/nginx/conf.d directory.
    # See http://nginx.org/en/docs/ngx_core_module.html#include
    # for more information.
    include /etc/nginx/conf.d/*.conf;
	upstream server	{
		server localhost:11
		server localhost:22
	}
    server {
        listen       80 default_server;
        server_name  _;
        root         /usr/share/nginx/html;

        # Load configuration files for the default server block.
        include /etc/nginx/default.d/*.conf;

        location / {
        }

        error_page 404 /404.html;
            location = /40x.html {
        }

        error_page 500 502 503 504 /50x.html;
            location = /50x.html {
        }
    }

# Settings for a TLS enabled server.
#
#    server {
#        listen       443 ssl http2 default_server;
#        listen       [::]:443 ssl http2 default_server;
#        server_name  _;
#        root         /usr/share/nginx/html;
#
#        ssl_certificate "/etc/pki/nginx/server.crt";
#        ssl_certificate_key "/etc/pki/nginx/private/server.key";
#        ssl_session_cache shared:SSL:1m;
#        ssl_session_timeout  10m;
#        ssl_ciphers HIGH:!aNULL:!MD5;
#        ssl_prefer_server_ciphers on;
#
#        # Load configuration files for the default server block.
#        include /etc/nginx/default.d/*.conf;
#
#        location / {
#        }
#
#        error_page 404 /404.html;
#            location = /40x.html {
#        }
#
#        error_page 500 502 503 504 /50x.html;
#            location = /50x.html {
#        }
#    }

}

```

#### location 

##### [=] 修饰符：要求路径完全匹配

```shell
server{
	server_name website.com
	location = /abcd {
	
	}
}
```

##### 请求

+ `http://website.com/abcd `**匹配** 

+ `http://website.com/ABCD`**可能会匹配** ，也可以不匹配，取决于操作系统的文件系统是否大小

  写敏感（case-sensitive）。ps: Mac 默认是大小写不敏感的，git 使用会有大坑。

+ `http://website.com/abcd?param1&param2`**匹配**，忽略 querystring

+ `http://website.com/abcd/`**不匹配**，带有结尾的`/`

+ `http://website.com/abcde`**不匹配**

##### 「~」修饰符：区分大小写的正则匹配 

##### 「~*」不区分大小写的正则匹配

> ^/abcd$`这个正则表达式表示字符串必须以`/`开始，以`$`结束，中间必须是`abcd

```shell
server {
    server_name website.com;
    location ~ ^/abcd$ {
    […]
    }
}
```

+ ` http://website.com/abcd`**匹配**（完全匹配）

+ `http://website.com/ABCD`**不匹配**，大小写敏感

+ `http://website.com/abcd?param1&param2`**匹配**

+  `http://website.com/abcd/`**不匹配**，不能匹配正则表达式

+ `http://website.com/abcde`**不匹配**，不能匹配正则表达式

##### 「^~」修饰符

> 前缀匹配 如果该 location 是最佳的匹配，那么对于匹配这个 location 的字符串， 该修饰符不再进行正则表达式检测。注意，这不是一个正则表达式匹配，它的目的是优先于正则表达式的匹配

#### 查找的优先级

>```
>先精准匹配 = ，精准匹配成功则会立即停止其他类型匹配；
>没有精准匹配成功时，进行前缀匹配。先查找带有 ^~ 的前缀匹配，带有 ^~ 的前缀匹配成功则立即停止其他类型匹配，普通前缀匹配（不带参数 ^~ ）成功则会暂存，继续查找正则匹配；
>= 和 ^~ 均未匹配成功前提下，查找正则匹配 ~ 和 ~* 。当同时有多个正则匹配时，按其在配置文件中出现的先后顺序优先匹配，命中则立即停止其他类型匹配；
>所有正则匹配均未成功时，返回步骤 2 中暂存的普通前缀匹配（不带参数 ^~ ）结果
>
>1. location =    # 精准匹配
>2. location ^~   # 带参前缀匹配
>3. location ~    # 正则匹配（区分大小写）【按顺序】
>4. location ~*   # 正则匹配（不区分大小写）
>5. location /a   # 普通前缀匹配，优先级低于带参数前缀匹配。
>6. location /    # 任何没有匹配成功的，都会匹配这里处理
>```

#### 路径拼接

```shell
 location ^~/order/ {
        proxy_set_header Host $host;
        proxy_set_header  X-Real-IP        $remote_addr;
        proxy_set_header  X-Forwarded-For  $proxy_add_x_forwarded_for;
        proxy_set_header X-NginX-Proxy true;

        proxy_pass http://127.0.0.1/
```

```
请求：localhost:8081/order/test
结果：localhost:8081/test
```

结尾有`/`，则会去除order

#### vue 相关配置

nginx正确的配置：

1、如果是在根目录则配置如下

```shell
location / {
　　root /；
　　index index.html;
　　try_files $uri $uri/ /index.html
}
```

2.如果是有特定目录

```shell
location /xx/xx/ {
　　root /;
　　index index.html;
　　try_files $uri $uri/ /xx/xx/index.html
}
```

####  alias  与 root

```
alias中，如果location后面带“/”结束（如：location /img/），则alias后面也必须要用“/”结束。
如果location后面不带“/”结束（如：location /img），则alias后面也必须没有，否则会找不到文件的。。。
```

#### 前端静态资源跨域问题

```shell
 add_header Access-Control-Allow-Origin '*';
 add_header Access-Control-Allow-Methods 'GET, POST, PUT, OPTIONS';
 add_header Access-Control-Expose-Headers 'Accept-Ranges, Content-Encoding, Content-Length, Content-Range';
```

