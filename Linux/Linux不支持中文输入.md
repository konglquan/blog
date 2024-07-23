而此时，svn checkout 或者 svn ci 时，有中文命名的文件时，会提示

**Can't convert string from 'UTF-8' to native encoding**

于是找到此方法：

1.修改 .bash_profile 文件，添加如下代码：

```
export LC_ALL=en_US.UTF-8
export LANG=en_US.UTF-8
 	
```

 

2.source一下

. ~/.bashrc







```
vim ~/.bashrc
source ~/.bashrc
```

```
export LC_ALL=en_US.UTF-8
export LANG=en_US.UTF-8
export LANGUAGE=en_US.UTF-8
```

======================





1. 设置系统语言环境:

	- 以 Ubuntu 为例,编辑 `/etc/environment` 文件,添加或修改 `LANG` 和 `LANGUAGE` 环境变量:

		复制

		```
		LANG="zh_CN.UTF-8"
		LANGUAGE="zh_CN:zh:en_US:en"
		```

	- 保存文件并退出。

2. 更新系统语言环境:

	- 运行 `sudo locale-gen zh_CN.UTF-8` 生成中文语言环境。
	- 运行 `sudo update-locale LANG=zh_CN.UTF-8` 更新系统语言环境设置。
