## mysql

### 1.SQL分类

 ####  DDL（data definition language）数据库定义语言

> 创建表的时候用到的一些sql，比如说：CREATE、ALTER、DROP，主要是用在定义或改变表的结构，数据类型，表之间的链接和约束等初始化工作上

#### DML（data manipulation language）数据操纵语

> 如：SELECT、UPDATE、INSERT、DELETE，主要用来对数据库的数据进行一些操作。

#### DCL（Data Control Language）：数据控制语句

> 用于控制不同数据段直接的许可和访问级别的语句。这些语句定义了数据库、表、字段、用户的访问权限和安全级别。主要的语句关键字包括 grant、revoke 等。

### 2.帮助语句

```mysql
用“？contents”命令来显示所有可供查询的的分类
```

字符序校对

```mysql
校对规则命名约定：它们以其相关的字符集名开始，通常包括一个语言名，并且以_ci
（大小写不敏感）、_cs（大小写敏感）或_bin（二元，即比较是基于字符编码的值而与language
无关）结束。
```



- **一条SQL语句执行得很慢的原因有哪些？**
- 大多数情况是正常的，只是偶尔会出现很慢的情况。
    - 数据库在刷新脏页(flush)
    - 在数据量不变的情况下，这条SQL语句一直以来都执行的很慢

---

- **查看表的状态锁**

  1、show processlist

---

- **事务（ACID）**

  1、原子性（Acomicity）

  2、一致性(Consistency)

  3、隔离性(Isolation)

  4、持久性(Durability)

- 事务隔离离别

  - 查看事务隔离级别：select @@tx_isolation
  - 设置事务隔离级别：set transaction isolation level read committed;
  - 设置数据库系统的全局的隔离级别：set global transaciton isolation ``
  
- 查看linux 下mysql相关数据

  ```shell
  show variables like '%dir%';
  ```


### 三大范式

1、 拆字段

2、满足第一范式的前提下，



#### 字符集 字符序

>字符集（character set）：定义了字符以及字符的编码。
>
>字符序（collation）：定义了字符的比较规则。

ex:

```
有四个字符：A、B、a、b，这四个字符的编码分别是A = 0, B = 1, a = 2, b = 3。这里的字符 + 编码就构成了字符集（character set）。

如果我们想比较两个字符的大小呢？比如A、B，或者a、b，最直观的比较方式是采用它们的编码，比如因为0 < 1，所以 A < B。

另外，对于A、a，虽然它们编码不同，但我们觉得大小写字符应该是相等的，也就是说 A == a。

这上面定义了两条比较规则，这些比较规则的集合就是collation。

同样是大写字符、小写字符，则比较他们的编码大小；
如果两个字符为大小写关系，则它们相等。
```

```
character_set_client：客户端请求数据的字符集

character_set_connection：客户机与服务器连接的字符集

character_set_database：默认数据库的字符集；如果没有默认数据库，就会使用 character_set_server指定的字符集（建议不要随意更改）

character_set_filesystem：把 character_set_client转换character_set_filesystem (默认为binary, 不做任何转换)

character_set_results：返回给客户端的字符集

character_set_server：数据库服务器的默认字符集

character_set_system：系统字符集，默认utf8。（用于数据库的表、列和存储在目录表中函数的名字）

character_sets_dir：mysql字符集文件的保存路径
```
### 字符编码
```mysql
查看可用的字符集
SHOW CHARACTER SET;
查看字符序
SHOW COLLATION
#字符编码
show variables like '%char%'
#字符编码统一设置为utf-8
vim /etc/my.cnf
[mysql]
default-character-set=utf8
[client]
default-character-set=utf8
[mysqld]
character_set_server=utf8
character_set_client=utf8
#字符排序
collaction_server=utf8_general_ci

```

==注意：修改编码只对**之后**创建的数据库生效，因此建议安装完之后就对其设置==

```shell
#启动
service mysql start
#停用
service mysql stop
#重启
service mysql restart
```

### 分层

+ 连接层：提供与客户端链接的服务
+ 服务层：1、提供各种用户使用的接口（select）2、提供SQL优化器（MySQL QUery Optimizer）
+ 引擎层：提供了各种村粗数据的方式（InnoDB MyISAM）
+ 存储层：存储数据

#### 查询数据库引擎

```mysql
show engines \g  or ;
```

