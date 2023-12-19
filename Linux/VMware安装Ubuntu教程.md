# VMware安装Ubuntu教程

## 一、VMware操作

### 1、采用经典安装

![image-20231210145745618](imgs/image-20231210145745618.png)

### 2、选择镜像

![image-20231210145802313](imgs/image-20231210145802313.png)

### 3、设置相关信息

![image-20231210145835463](imgs/image-20231210145835463.png)

### 4、设置虚拟机名

![image-20231210145909859](imgs/image-20231210145909859.png)

### 5、指定磁盘容量

![image-20231210145926743](imgs/image-20231210145926743.png)

### 6、设置内存

![image-20231210145950001](imgs/image-20231210145950001.png)

## 二、Ubuntu系统内操作

### 1、选择语言

这里直接Continue

![image-20231210150200693](imgs/image-20231210150200693.png)

### 2、软件安装

这里直接Continue，然后等待。

![image-20231210150305583](imgs/image-20231210150305583.png)



### 3、选择安装类型

这里直接Instal Now，然后等待。

![image-20231210150438209](imgs/image-20231210150438209.png)

### 4、选择时区

这里选择 上海，然后Continue。

![image-20231210150649275](imgs/image-20231210150649275.png)

### 5、设置用户名密码

填写系统名、用户名、密码，然后Continue，这里等待比较久。

![image-20231210150809392](imgs/image-20231210150809392.png)

### 6、重启

加载完成后需要重启

## 三、系统配置【重要】

### 1、安装ssh

```shell
sudo apt update
sudo apt install openssh-server
```

### 2、配置root密码

```shell
sudo passwd root
```

### 3、配置apt-get源

清华源：https://mirrors.tuna.tsinghua.edu.cn/help/ubuntu/

- 修改镜像源，打开配置文件，将镜像源链接粘贴到配置文件

```shell
sudo mv /etc/apt/sources.list /etc/apt/sources.list_bak
sudo vi /etc/apt/sources.list
```

vim后粘贴这个

![image-20231209174659893](imgs/image-20231209174659893.png)

- 更新软件列表到本地

```shell
sudo apt-get update
```

- 更新所有软件（非必要）

```shell
sudp apt-get upgrade
```

### 4、配置静态IP地址

#### 方法一：可视化配置

##### 1、进入设置

![image-20231210152341042](imgs/image-20231210152341042.png)

##### 2、网卡设置

![image-20231210152426900](imgs/image-20231210152426900.png)

##### 3、设置IP以及网关

注：网关以及网段要配置一致

![image-20231210152900255](imgs/image-20231210152900255.png)

##### 4、重启网卡

![image-20231210152815145](imgs/image-20231210152815145.png)

##### 5、效果

![image-20231210152942372](imgs/image-20231210152942372.png)

#### 方法二：命令行

```shell
# 查看网卡
ip a
# 进入配置文件所在目录
cd /etc/netplan
# 查看目录下的内容
ls
# 备份配置
sudo cp 01-network-manager-all.yaml 01-network-manager-all.yaml_bak
# 打开配置文件进行修改
sudo vim 01-network-manager-all.yaml

network:
  ethernets:
    ens33:
      addresses: [192.168.200.52/24]          	# 设置静态IP地址和掩码
      gateway4: 192.168.200.1             		# 设置网关地址
      dhcp4: false                            	# 禁用dhcp
      nameservers:
        addresses: [114.114.114.114, 8.8.8.8] # 设置主、备DNS
  version: 2
  renderer: NetworkManager
```