## linux

>1. 基本操作命令
>2. 配置(环境变量配置，网络配置，服务配置)
>3. Linux下如何搭建对应语言的开发环境
>4. 编写shell 脚本
>5. 安全设置，防止攻击，保障服务器正常运行，系统调优
>6. 深入理解Linux系统。

### 1.目录结构

|      目录      |                             说明                             |
| :------------: | :----------------------------------------------------------: |
|    **bin**     |               是Binary 的缩写，存放常用的命令                |
|    **sbin**    |        super user ，存放系统管理员使用的系统管理程序         |
|    **home**    | 存放普通用户的主目录，每个用户都有一个自己的目录，一般该目录名是以用户的账号命名 |
|    **root**    |              系统管理员，超级权限者的用户主目录              |
|    **lib**     | 系统开机所需要最基本的动态链接共享库，作用类十余windows里 的DDL文件，几乎所有的应用程序都会用到 |
| **lost+found** |         一般为空，当系统非法关系后，这个存放一些文件         |
|    **etc**     |             所有的系统管理所需要的配置文件和目录             |
|    **usr**     | 存放用户的应用程序和文武兼都放在这个目录下，类似于windows下的program files目录 |
|    **boot**    | 存放启动linux时使用的一些核心文件，包括一些链接文件以及文件  |
|    **proc**    |     虚拟目录，系统内存的映射，访问这个目录来获取系统信息     |
|    **srv**     |    service缩写，该目录存放一些服务启动之后需要提取的数据     |
|    **sys**     |                   2.6之后新的一个文件系统                    |
|    **tmp**     |                         存放临时文件                         |
|    **dev**     |    类似Windows的设备管理器，把所以的硬件用文件的形式存储     |
|   **media**    | 系统会自动是被一些设备，如U盘、光驱等，当识别后，系统会把识别的设备挂载到这个目录下 |
|    **mnt**     | 系统提供该目录是为了让用户临时挂载别的文件系统的，我们可以将外部的存储挂载在mnt上，然后进入该目录就可以查看里面的内容。 |
|    **opt**     |                      软件下载存放的目录                      |
| **usr/local**  |                      软件安装的最终目录                      |
|    **var**     | 存放着不断扩充着的东西，系统将精彩被修改的目录放在这个目录下，包括各种日志文件 |
|  **selinux**   |            安全子系统，控制程序只能访问特定文件。            |
|                |                                                              |

### 2.远程登录linux

+ xshell
+ xFtp
+ finalShell

### 3.常用指令

```
yum -y list java* 列出所有的java 
yum install xx 安装某个软件
```

### 4.压缩命令

```shell
.gz ： gzip ； gunzip(gzip -d) #gzip的压缩和解压都是不保留原文件的。而且是不支持对文件夹的压缩的
.tar ： tar -cf ； tar -xf
.tar.gz ： tar -zcf ； tar -zxf
	-c ：打包
	-x ：解包
	-v ：显示详细信息
	-f ：指定文件名
	-z ：打包同时压缩
.zip ： zip -r ； unzip
.bz2 ：bzip2 ； bunzip2
.tar.bz2 ：tar -cjf ； tar -xjf
```

