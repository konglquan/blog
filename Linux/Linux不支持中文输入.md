而此时，svn checkout 或者 svn ci 时，有中文命名的文件时，会提示

**Can't convert string from 'UTF-8' to native encoding**

于是找到此方法：

1.修改 .bash_profile 文件，添加如下代码：

export LC_ALL=en_US.UTF-8
export LANG=en_US.UTF-8
export LANGUAGE=en_US.UTF-8

 

2.source一下

. ~/.bashrc