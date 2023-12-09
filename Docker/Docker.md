# Docker

## Docker安装

### Docker官网

```
www.docker.com
```

### Ubuntu系统

```
https://docs.docker.com/engine/install/ubuntu/
```

### CentOS

```
https://docs.docker.com/engine/install/centos/
```



### Docker切换镜像源

Docker官方镜像：
“https://registry.docker-cn.com”

网易镜像：
“http://hub-mirror.c.163.com”

中国科技大学镜像：
“https://docker.mirrors.ustc.edu.cn”

阿里云镜像：
“https://cr.console.aliyun.com”

腾讯云镜像：
“https://mirror.ccs.tencentyun.com”

```shell
sudo vi /etc/docker/daemon.json
```

```json
{
  "registry-mirrors": [
    "https://docker.mirrors.ustc.edu.cn"
  ]
}
```

重启

```shell
sudo systemctl daemon-reload
sudo systemctl restart docker
```





## MySQL容器部署

1、搜索mysql镜像

```shell
docker search mysql
```

2、拉取mysql镜像

```shell
docker pull mysql:8.0.25
```

3、创建容器，设置端口映射、目录映射

```shell
# 在/root目录下创建mysql目录用于存储mysql数据信息
mkdir -p /home/kong/software/mysql
cd /home/kong/software/mysql
```

```shell
docker run -id \
-p 3306:3306 \
--name=mysql \
-v /home/kong/software/mysql/conf:/etc/mysql/conf.d \
-v /home/kong/software/mysql/logs:/logs \
-v /home/kong/software/mysql/data:/var/lib/mysql \
-e MYSQL_ROOT_PASSWORD=root \
mysql:8.0.25
```

- 参数说明：
	- **-p 3306:3306**：将容器的 3306 端口映射到宿主机的 3306	 端口。
	- **-v $PWD/conf:/etc/mysql/conf.d**：将主机当前目录下的 conf/my.cnf 挂载到容器的 /etc/mysql/my.cnf。配置目录
	- **-v $PWD/logs:/logs**：将主机当前目录下的 logs 目录挂载到容器的 /logs。日志目录
	- **-v $PWD/data:/var/lib/mysql** ：将主机当前目录下的data目录挂载到容器的 /var/lib/mysql 。数据目录
	- **-e MYSQL_ROOT_PASSWORD=root：**初始化 root 用户的密码。

4、进入容器，操作mysql

```shell
docker exec -it mysql /bin/bash
```

注：如果需要在docker启动时自动启动容器，再运行一个docker的命令即可

```
docker update mysql --restart=always
```

## Redis容器部署

1、搜索redis镜像

```shell
docker search redis
```

2、拉取redis镜像

```shell
docker pull redis:6.0.9
```

3、创建容器，设置端口映射

```
docker run -id --name=redis -p 6379:6379 redis:6.0.9
```

```
# 运行redis容器，并指定密码
docker run -id --name=redis -p 6379:6379 redis:6.0.9 --requirepass "123456"
```

- 参数说明

	- name：指定容器的名字，这个名字是唯一的。

	- -p：做端口映射，6379:6379，前一个端口是指的安装docker的宿主机的端口，后一个端口指的是docker容器的端口。如果在同一个宿主机上，要启动多个redis容器实例的话，就需要修改前一个端口号。

	- -d：表示在后台启动容器

	- --requirepass：redis的配置参数，这里指的是redis访问密码。

4、使用外部机器连接redis

```shell
./redis-cli.exe -h 192.168.200.101 -p 6379
```

注：如果需要在docker启动时自动启动容器，再运行一个docker的命令即可

```
docker update redis --restart=always
```

## ElasticSearch容器部署

