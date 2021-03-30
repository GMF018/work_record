## Elasticsearch

> Elasticsearch 是一个分布式、高扩展、高实时的搜索与[数据分析](https://baike.baidu.com/item/数据分析/6577123)引擎。它能很方便的使大量数据具有搜索、分析和探索的能力

### 官网

>https://www.elastic.co/guide/en/elasticsearch/reference/7.9/rpm.html#rpm-key

#### 安装 

+ 下载并安装公共签名秘钥

```shell
rpm --import https://artifacts.elastic.co/GPG-KEY-elasticsearch
```

+ 从RPM存储库安装，在 /etc/yum.repos.d/目录下创建elasticsearch.repo,其内容包含

```shell
[elasticsearch]
name=Elasticsearch repository for 7.x packages
baseurl=https://artifacts.elastic.co/packages/7.x/yum
gpgcheck=1
gpgkey=https://artifacts.elastic.co/GPG-KEY-elasticsearch
enabled=0
autorefresh=1
type=rpm-md
```

+ 初始化

```shell
sudo yum install --enablerepo=elasticsearch elasticsearch
```

+ 启动

```shell 
sudo /bin/systemctl daemon-reload
sudo /bin/systemctl enable elasticsearch.service

sudo systemctl start elasticsearch.service
sudo systemctl stop elasticsearch.service

```

+ 相关目录

```shell
/var/log/elasticsearch/ #日志查看
/etc/elasticsearch      #配置
```

+ 密码库密码保护

```shell
echo "keystore_password" > /path/to/my_pwd_file.tmp
chmod 600 /path/to/my_pwd_file.tmp
sudo systemctl set-environment ES_KEYSTORE_PASSPHRASE_FILE=/path/to/my_pwd_file.tmp
sudo systemctl start elasticsearch.service
```

+ 检查是否运行

```
GET /localost:9200

{
  "name" : "Cp8oag6",
  "cluster_name" : "elasticsearch",
  "cluster_uuid" : "AT69_T_DTp-1qgIJlatQqA",
  "version" : {
    "number" : "7.9.3",
    "build_flavor" : "default",
    "build_type" : "tar",
    "build_hash" : "f27399d",
    "build_date" : "2016-03-30T09:51:41.449Z",
    "build_snapshot" : false,
    "lucene_version" : "8.6.2",
    "minimum_wire_compatibility_version" : "1.2.3",
    "minimum_index_compatibility_version" : "1.2.3"
  },
  "tagline" : "You Know, for Search"
}
```

