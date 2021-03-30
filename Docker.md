## Docker

> 容器化技术：
>
> 虚拟机技术缺点：
>
> 1、资源占用十分多
>
> 2、冗余步骤多
>
> 3、启动慢

#### Docker和虚拟机技术的不同

+ 传统虚拟机，虚拟出一个硬件，运行ing一个完整 的操作系统个，然后在装个系统上安装和运行软件
+ 容器内的应用相直接运行在宿主的内核，本身没有自己的内核，也没有虚拟我们的硬件，所以比较轻巧
+ 容器之间相互隔离，都有属于自己的文件系统，互不影响。

##### 列出镜像列表

```
docker images
```

##### 获取新的镜像

```
docker pull centos:7.0
```

#####  查找镜像

```
docker seach httpd
```

##### 更新镜像

```
docker commit -m="提交的信息" -a ="作者" ···
```

##### 删除镜像

```
docker rmi 49c614fbbea8

Error response from daemon: conflict: unable to delete 49c614fbbea8 (must be forced) - image is referenced in multiple repositories

# 这个报错说明它被其他的镜像依赖，所以需要先删除依赖的image


[root@FantJ ~]# docker rmi 49c614fbbea8
Error response from daemon: conflict: unable to delete 49c614fbbea8 (must be forced) - image is being used by stopped container ffd74d6603e0

#这个报错说明它被容器所使用，所以需要先删除容器
[root@FantJ ~]# docker rm ffd74d6603e0
ffd74d6603e0


#如果发现它被很多个容器占用，就用批量命令
[root@FantJ ~]# docker rm $(docker ps -a -q)
27298d317f59
955bbef03be9
95889edc40c8
518eff5fed00
c0b7ca7b267b
ce5935dfa127
63c212771b1e
906780ebb103
[root@FantJ ~]# docker rmi 49c614fbbea8
Untagged: learn/pingtag:latest
Deleted: sha256:49c614fbbea80b328834ecde9a39d8f5bb812c32851e0e5ae39b514642426984
Deleted: sha256:1de562b8b13c8b7af429a9072ef19a35e3c9085a202ffee5ed5c8aef4046cad4

```

##### 运行容器

```shell
-d 后台运行
--restart=always 开机自启
-p 外部端口：内部端口
```

##### 查看容器挂载目录

```shell
docker ps -a
docker inspect container_id | grep Mounts -A 20
docker inspect container_name | grep Mounts -A 20
```
##### 镜像自启动

```shell
docker update --restart=always 你的镜像名称/id
```

##### 关闭镜像自启动

```shell
docker update –restart=no <CONTAINER ID>
```

##### 查看容器映射

```shell
docker inspect mysql5.7 | grep Mounts -A 20
```

#### 安装并运行

```shell
docker run -u root-d --restart=always -p 8099:8080 -p 50000:50000 -name jenkins -v jenkins-data:/var/jenkins_home -v /var/run/docker.sock:/var/run/docker.sock jenkinsci/blueocean 
```

### 常用软件安装

#### mysql

```shell
docker run --restart=always --name mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=root -e TZ=Asia/Shanghai -v /docker_data/mysql/log:/var/log/mysql -v /docker_data/mysql/data:/var/lib/mysql -v /docker_data/mysql/conf:/etc/mysql -d mysql:5.7  --character-set-server=utf8mb4 --collation-server=utf8mb4_unicode_ci --default-time_zone='+8:00'
```

#### redis

```shell
mkdir -p /docker_data/reids/conf
touch /docker_data/redis/conf/redis.conf

docker run --restart=always --name redis -v /docker_data/redis/data:/data \
-v /docker_data/redis/conf/redis.conf:/etc/redis/redis.conf \
-d redis redis-server /etc/redis/redis.conf

#进入容器
docker exec -it redis redis-cli
#redis 持久化
vim redis.conf
appendonly yes
```



