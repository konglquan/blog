# Linux通过rm删除文件空间并未释放

##### 第一种方法：关闭进程

如果有什么不能解决的问题，那就重启下服务吧。

使用 rm -rf x.log 删除后，但是因服务仍在运行，空间不会立刻释放，需要重启或停止服务才能将空间释放。

可是线上可不能这样操作，该怎么办？



```shell
echo "">a.log
# 使用带有空字符串的echo命令，并将其重定向到文件
```



```shell
truncate -s 0 x.log
# 指定目标文件字符大小为0
```



```shell
cp /dev/null x.log
# copy /dev/null 至 x.log文件

cat /dev/null> x.log
# cat + 重定向 /dev/null 至 x.log文件

dd if=/dev/null of=x.log
# dd 转换/dev/null 至 x.log
```



如果已经删了怎么办呢？

通过`lsof` 命令可以查看所有打开的文件，显示有关进程和它们打开的文件的详细信息，这对于解决与文件访问有关的问题或识别消耗系统资源的进程有很大的帮助

几个常用的例子：

- 列出所有打开的文件：`lsof`
- 列出特定进程的所有打开文件：`lsof -p <PID>`
- 列出特定用户的所有打开文件：`lsof -u <username>`
- 列出特定端口的所有打开文件：`lsof -i :<PORT>`
- 列出特定文件的所有打开文件：`lsof /PATH/to/FILE`

通过`lsof -n | grep deleted`命令列出所有已经被删除但是仍然被一个或多个进程保持打开状态的文件

**建议使用正常方法退出进程，让系统自动回收磁盘空间**

不建议重启系统、强制结束进程但也可以通过`echo "" > /path/to/file`清空文件