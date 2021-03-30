# Jenkins

### CentOS 7

#### 第一种方式

```shell
sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key

yum install jenkins
```

#### 第二种方式

```sh
wget https://pkg.jenkins.io/redhat/jenkins-2.156-1.1.noarch.rpm
rpm -ivh jenkins-2.156-1.1.noarch.rpm
```

##### 配置

```shell
vim /etc/sysconfig/jenkins

# 监听端口
JENKINS_PORT="8080"
# JENKINS 目录位置
JENKINS_HOME="xxx"
# 修改权限配置
$JENKINS_USER="root"

# 修改目录权限
chown -R root:root /var/lib/jenkins
chown -R root:root /var/cache/jenkins
chown -R root:root /var/log/jenkins

service jenkins restart
ps -ef | grep jenkins
# 重启与启动
systemctl stop jenkins
systemctl start jenkins
systemctl restart jenkins
```

### Dokcer 方式


```
docker run -u root --restart=always -p 8088:8080 -p 50000:50000 --name jenkins -v /root/sdSoft/docker/data/jenkins:/var/jenkins_home jenkinsci/blueocean
```

### 错误问题

```shell
#错误信息为`Starting Jenkins bash: /usr/bin/java: No such file or directory`是java环境配置的问题。创建软连接
ln -s /usr/local/java/jdk1.8.0_171/bin/java /usr/bin/java

#Jenkins初始化插件失败
vim /var/lib/jenkins/hudson.model.UpdateCenter.xml
http://mirror.xmission.com/jenkins/updates/update-center.json

#账号密码忘记问题
一、admin密码未更改情况
1.进入\Jenkins\secrets目录，打开initialAdminPassword文件，复制密码；
2.访问Jenkins页面，输入管理员admin，及刚才的密码；
3.进入后可更改其他管理员密码；
二、admin密码更改忘记情况
1.删除Jenkins目录下config.xml文件中下面代码，并保存文件。
2.重启Jenkins服务；
3.进入首页>“系统管理”>“Configure Global Security”；
4.勾选“启用安全”；
5.点选“Jenkins专有用户数据库”，并点击“保存”；
6.重新点击首页>“系统管理”,发现此时出现“管理用户”；
7.点击进入展示“用户列表”；
8.点击右侧进入修改密码页面，修改后即可重新登录

```

### 执行脚本

```shell
npm config set registry http://registry.npm.taobao.org/ && 
cd bgy_back && npm install 
&& rm -rf dist && npm run build


case ${Status} in
  deploy)
    node -v
    npm -v
	cd bgy_back &&
	npm install &&
	npm run build
    echo "Status:$Status"
    path="${WORKSPACE}/bak/${BUILD_NUMBER}"    
    mkdir -p  $path
    \cp -R ${WORKSPACE}/back $path
    echo "Completing!"
    ;;
    
  roll_back)
    echo "status:$status"
    echo "version:$version"
	cd ${WORKSPACE}
    rm -rf dist/static
	rm -rf dist/index.html
    cd D:/publish/项目名称/bak/$version
    \cp -f index.html ${WORKSPACE}/dist/
    \cp -r static ${WORKSPACE}/dist/
     ;;
esac

```

### 查看内存占用情况

```shell
ps aux|head -1;ps aux|grep -v PID|sort -rn -k +4|head

```

























