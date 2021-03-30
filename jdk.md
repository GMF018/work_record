## JDK

官网：https://www.oracle.com/java/technologies/javase-downloads.html

#### 配置环境变量

（1）修改 /etc/profile，记得修改JDK 版本号

```shell
export JAVA_HOME=/usr/share/jdk1.6.0_14 
export PATH=$JAVA_HOME/bin:$PATH 
export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar 
```

(2)配置文件立即生效

```shell
source /etc/profile
```
