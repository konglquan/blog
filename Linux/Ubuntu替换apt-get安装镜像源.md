清华源：

https://mirrors.tuna.tsinghua.edu.cn/help/ubuntu/

- 修改镜像源，打开配置文件，将镜像源链接粘贴到配置文件

```shell
sudo mv /etc/apt/sources.list /etc/apt/sources.list_bak
sudo vim /etc/apt/sources.list
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