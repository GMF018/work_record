## Minio

### 1.下载

>wget https://dl.minio.io/server/minio/release/linux-amd64/minio

### 2.运行

> chmod +x minio
> #启动
> ./minio server /usr/software/minio/data
> 或者
> MINIO_ACCESS_KEY=myminioadmin MINIO_SECRET_KEY=myminioadmin ./minio server /usr/software/minio/data
> 或者
> MINIO_ACCESS_KEY=myminioadmin MINIO_SECRET_KEY=myminioadmin ./minio server --config-dir /usr/software/minio/config /usr/software/minio/data

### 3、后台启动

> #后台运行
> nohup ./minio server /usr/software/minio/data  >  /usr/software/minio/minio.log 2>&1 &##或者
> MINIO_ACCESS_KEY=myminioadmin MINIO_SECRET_KEY=myminioadmin nohup ./minio server --config-dir /usr/software/minio/config /usr/software/minio/data>  /usr/software/minio/minio.log 2>&1 &#

### 4、测试

> http://ip:9000


```shell
nohup ./minio server --address 0.0.0.0:19000 http://10.208.18.72/data/soft/minio/data http://10.208.18.72/data/soft/minio/data1 \
                http://10.208.18.143/data/soft/minio/data http://10.208.18.143/data/soft/minio/data1 >/dev/null 2>&1 &
#后台运行 minio软件位置 默认地址 数据存放 日志地址  			  
nohup ./minio server --address 0.0.0.0:19000 ./data >./minio.log 2>&1 &		
```

### 5、docker 安装

```shell
docker run -p 9000:9000 --name minio \
-d --restart=always \
-e "MINIO_ACCESS_KEY=admin" \
-e "MINIO_SECRET_KEY=admin123456" \
-v /home/data:/data \
-v /home/config:/root/.minio \
minio/minio server /data
```

