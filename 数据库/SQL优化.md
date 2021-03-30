## MySQL优化

#### 原因

> 性能低、执行时间长、等待时间长、SQL语句欠佳（连接查询）、索引失效、服务器参数不合理（缓冲区、线程数）
>
> 官网：https://dev.mysql.com/doc/refman/5.7/en/optimization.html

#### 编写过程

```mysql
select distinct ..from .. join ..on ..where.. group by..having..order by ..limit..
```

#### 解析过程

```mysql
from..on..join..where..group by...having..select distinct ..order by ..limit..
```

==SQL优化：主要就是优化索引==

**索引：相当于书的目录  index是帮助MySQL搞笑获取数据的数据结构。索引是数据结构（B+tree）**

索引的弊端：

​	1、索引本身很大、可以存放在内存、硬盘

​	2、索引不是所有情况均适用：a.少了数据 b.频繁更新的字段 c.很少适用的字段

​	3、索引回降低增删改的效率

索引的优势：

​	1、提高查询的效率（降低IO使用率）

​	2、降低CPU使用率、

```mysql
#单值索引
create index dept_index on 表（字段）
或
alter table 表名 add index dept_index(字段)
#唯一索引
create unique index name_index on 表（字段）
alter table 表名 add unique index dept_index(字段)
#符合索引
create  index name_index on 表（字段,字段）
alter table 表名 add  index dept_index(字段,字段)

#删除索引：
drop index 索引名 on table
#查询索引
show index from table
```

### 索引类型

```mysql
system/const:结果只有一条数据；
eq_ref:结果多条，但是每天数据是唯一的；
ref：结果多条，但是每条数据是0或多条；
```

#### 表优化

```mysql
#两表优化
原则：小白驱动大表
```

##### 慢查询日志

> 用于记录MySQL中相应时间超过阈值的SQL语句（long_query_time 默认10s）

**检查是否开启了慢查询日志**

```mysql
show variables like 'slow_query_log';
```

**临时开启**

```mysql
set global slow_query_log=1;
```

永久开启

```shell
slow_query_log=1
slow_query_log_file=目录
```

