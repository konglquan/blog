# JDK

## 解压

```
tar -xvf jdk8.tar.gz -C /home/cntd/dir_install/
```



## 配置环境变量

/home/install/jdk1.8.0_144

```
vim /etc/profile
```

```
export JAVA_HOME=/home/install/jdk1.8.0_144
export PATH=$JAVA_HOME/bin:$PATH
export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
```

```
export JAVA_HOME=/home/zkqa/cntd/dir_install/jdk-11.0.18
export PATH=$JAVA_HOME/bin:$PATH
export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
```



## 重新加载配置

```
source /etc/profile
```



## 检查

```
java -version
```

# MySQL

参考文章

https://www.jianshu.com/p/ab869705d152

https://blog.csdn.net/weixin_52100990/article/details/123651474

https://blog.csdn.net/qq_36539042/article/details/125385002

sr.t>YVud7tC



卸载mariadb

```shell
yum list installed | grep mariadb
```

```shell
yum -y remove mariadb-libs.x86_64
```

下载

```
wget https://dev.mysql.com/get/Downloads/MySQL-8.0/mysql-8.0.20-linux-glibc2.12-x86_64.tar.xz
```

```
xz -d mysql-8.0.20-linux-glibc2.12-x86_64.tar.xz
 
tar xvf mysql-8.0.20-linux-glibc2.12-x86_64.tar
```

安装

```
/home/install/mysql-8.0.20-linux-glibc2.12-x86_64

/home/software/mysql-8.0.20-linux-glibc2.12-x86_64
```

```
vi /etc/my.cnf
```

```
[mysqld]
user=root
datadir=/home/install/mysql/data
basedir=/home/install/mysql
port=3306
max_connections=200
max_connect_errors=10
character-set-server=utf8
default-storage-engine=INNODB
default_authentication_plugin=mysql_native_password
lower_case_table_names=1
group_concat_max_len=102400

[mysql]
default-character-set=utf8

[client]
port=3306
default-character-set=utf8
```



```bash
chown -R mysql /home/software/mysql-8.0.20-linux-glibc2.12-x86_64/
chgrp -R mysql /home/software/mysql-8.0.20-linux-glibc2.12-x86_64/
```

```csharp
cat /home/cntd/dir_install/mysql-8.0.26-linux-glibc2.12-x86_64/mysqld.log
```



```
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'root@1234';
```

```
ALTER USER 'root'@'localhost' IDENTIFIED BY 'root@1234';
```

https://blog.csdn.net/qq_42702382/article/details/125347648

```
ALTER USER 'root'@'localhost' IDENTIFIED BY 'root@1234';

ALTER USER 'root'@'localhost' IDENTIFIED BY 'root@1234';


ALTER USER 'root'@'localhost' IDENTIFIED BY 'root@1234';
alter user 'root'@'%' identified with mysql_native_password by 'root@1234';

```

```bash
cp /home/cntd/dir_install/mysql-8.0.26-linux-glibc2.12-x86_64/support-files/mysql.server /etc/init.d/mysqld
```

```
export MYSQL_HOME=/home/cntd/dir_install/mysql-8.0.26-linux-glibc2.12-x86_64
export PATH=$PATH:$JAVA_HOME/bin:$MYSQL_HOME/bin
```



# Redis

## 下载

```
wget http://download.redis.io/releases/redis-6.2.7.tar.gz
```



## 解压

```
tar -xvf redis-6.2.7.tar.gz -C /home/cntd/dir_install/
```



## 进入src

```
cd ./redis-6.2.7/src/
```



## 编译

```
make
make install
```



## 启动

```
cd /usr/local/bin
```

```
./redis-server
```


```
- 其它指令和配置

  ```Shell
#1. 后台运行 指令后面带 & 代表后台运行
./redis-server &  
#2. 运行远程访问 
#   使用vi编辑，打开redis.conf文件 （以下是在配置文件中修改）
#==============
# 注释如下这行，目前仅运行127.0.0.1访问
bind 127.0.0.1
#  开启密码访问模式
requirepass pass
#===============
#3. 指定配置文件，启动redis    
./redis-server redis.conf & 

#4. 启动redis客户端和关闭服务器
./redis-cli
./redis-cli shutdown
#5.开放端口
firewall-cmd --zone=public --add-port=6379/tcp --permanent
#重新加载配置
firewall-cmd --reload
#查看是否有nginx的线程是否存在
ps -ef | grep nginx
netstat -an -t -u | grep 6379
```



# Nginx

https://blog.csdn.net/weixin_40444253/article/details/126283168

## 解压

```
tar -xvf nginx-1.12.2.tar.gz -C /home/cntd/dir_install/nginx
```



```Shell
#解压缩nginx
tar -xvf nginx-1.14.2.tar.gz 
#进入nginx目录
cd nginx-1.14.2
#安装配置 
./configure  
#编译

make     

make install   

cd /usr/local/nginx/sbin

./nginx

./nginx -s reload
./nginx -s stop
```



## 安装gcc

## 解压

```
tar -xvf gcc.tar.gz -C /home/cntd/dir_install/
```



## 安装

```
rpm -Uvh *.rpm --nodeps --force
```



# kafka

启动zk

```
nohup ./bin/zookeeper-server-start.sh ./config/zookeeper.properties >logs/zookeeper.log  &
```

kafka跟目录

```
cd /home/cntd/dir_install/kafka_2.12-2.8.0
```

启动kafka

```
./bin/kafka-server-start.sh -daemon config/server.properties
```

查看状态

```
bin/kafka-topics.sh --bootstrap-server 10.20.100.102:35421 --list
```

创建topic

```
# 创建名为test的主题
bin/kafka-topics.sh --create --bootstrap-server localhost:8087 --topic test
# 查看目前Kafka中的主题
bin/kafka-topics.sh --list --bootstrap-server 10.20.100.102:35421
```



生产

```
bin/kafka-console-producer.sh --broker-list localhost:9092 --topic test
```

消费

```
bin/kafka-console-consumer.sh --bootstrap-server 10.20.100.102:35421 --topic DataIpInfo --from-beginning
```



```
/home/cntd/dir_install/kafka_2.12-2.8.0
```

删除主题

```
bin/kafka-topics.sh --delete --zookeeper localhost:2181 --topic cntd_vulnerability
```



```
221.216.205.22 kafka-1
```



```
如果不配置advertised.listeners=PLAINTEXT://101.89.163.1:9092，
你会发现虽然你给kafka客户端配置的访问地址是101.89.163.1:9092，但是kafka客户端访问时报错，报错原因是Connection to node -1[192.168.0.213:9092] could not be established. Broker may not be available.。这就是因为不配置advertised.listeners则advertised.listeners默认使用listeners配置的地址，客户端拿到的就是listeners配置的内网地址
```

https://www.cnblogs.com/gentlescholar/p/15179258.html

```
listeners=PLAINTEXT://10.20.100.102:8087
advertised.listeners=PLAINTEXT://221.216.205.22:35421
```

https://huaweicloud.csdn.net/637f7b76dacf622b8df85ab4.html?spm=1001.2101.3001.6661.1&utm_medium=distribute.pc_relevant_t0.none-task-blog-2~default~CTRLIST~activity-1-118734362-blog-127609013.pc_relevant_3mothn_strategy_and_data_recovery&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-2~default~CTRLIST~activity-1-118734362-blog-127609013.pc_relevant_3mothn_strategy_and_data_recovery&utm_relevant_index=1



https://www.cnblogs.com/gentlescholar/p/15179258.html

# samba

服务端

```
172.31.1.38
```

## 服务端配置

```
172.31.60.20
```

强制安装

```
rpm -ivh *.rpm --nodeps

rpm -ivh samba-4.10.16-24.el7_9.x86_64.rpm.rpm --nodeps
samba-4.10.16-24.el7_9.x86_64.rpm
```

启动

```
systemctl start smb nmb
```

查看系统是否安装了samba

```
rpm -qa | grep samba
```

添加用户

```
useradd zkqa123
```

添加用户并设置密码

```
smbpasswd -a zkqa123
```

同步目录

```
/home/cntd/file_syn
```

编辑配置

```
vim /etc/samba/smb.conf
```

增加



```
[zkqa123]
	comment = zkqa123
	path = /home/cntd/file_syn/
	security = user
	passdb backend = smbpasswd
	browseable = yes
	guest ok = no
	valid users = zkqa123
	writable = no
	write list = zkqa123
```

​		

给权限

```
setfacl -m u:zkqa123:rwx /home/cntd/file_syn/
```

```
chmod 777 -R /home/cntd/file_syn/
```

重启

```
systemctl restart smb nmb
```

可能用到的命令		

```
mount -t cifs //172.31.1.38/test /home/tmp/test -o username=test,password=test
					
mount -t cifs  //172.31.1.38/test /home/tmp/test cifs multiuser,username=test,password=test

vim /etc/fstab
//172.31.1.38/test /home/tmp/test cifs multiuser,username=test,password=test,sec=ntlmssp,_netdev 0 0
```

下载软件包到指定文件

```
yum install samba --downloadonly --downloaddir=/test -y
yum install gnutls  --downloadonly --downloaddir=/test -y
```

## 客户端配置

```
172.31.1.37
```

安装

```
yum -y install samba-client
```

强制安装

```
rpm -ivh *.rpm --nodeps
```

- 查看有哪些共享资源

```
smbclient -L [HOST] -U [USERNAME]   //查询共享资源
smbclient -L 172.31.60.20 -U zkqa123
smbclient -L 172.31.1.37 -U zkqa123


smbclient -L 192.168.1.51 -U cntdsmb
smbclient  //192.168.1.51/cntdsmb -U cntdsmb
```

查看共享文件夹位置

```
smbclient //server/shared_name -U USERNAME   //访问共享资源
smbclient //172.31.60.20/zkqa123 -U zkqa123

smbclient //172.31.1.37/zkqa123 -U zkqa123
59.255.104.87
```

安装 cifs

```
yum -y install cifs-utils
```

同步目录

```
/home/cntd/file_syn
```

挂载目录

```
mount -t cifs //172.31.60.20/zkqa123
```

```
mount -t cifs //172.31.60.20/zkqa123 /home/cntd/file_syn -o username=zkqa123,password=jksadGYod!#d3
```

查看挂载

```
df -h
```

在 /etc/fstab  文末增加如下内容

```
//172.31.60.20/zkqa123 /home/cntd/file_syn cifs multiuser,username=zkqa123,password=jksadGYod!#d3,sec=ntlmssp,_netdev 0 0
```

```
mount -a
```

查看挂载

```
df -h
```





## 修改端口

```
vim /etc/samba/smb.conf
```

在全局增加如下内容

```
smb ports = 4445
```

重启服务

```
systemctl restart smb nmb
```



## logstash

模板

```
input{
       elasticsearch{
            hosts => "10.20.100.102:9200"
            index => "cntd_data_dns_2021_07"
            query => '{"query":{"match_all":{}}}'
            size => 5000
            scroll => "5m"            
            user => "elastic"
            password => "ff#IST@QA1203"
       }
}
filter{
      mutate {
            remove_field => ["@version","@timestamp"]
     }
    
}
output{
      file{
          path => "/home/cntd/info/cntd_data_dns_2021_07.txt"
      } 
}

```

命令

```
bin/logstash -f config/cntd_data_ssl_certificate2023-04.conf --path.data=/home/cntd/info/conf/cntd_data_ssl_certificate2023-04 &
```

