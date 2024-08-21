## 挂载硬盘

```shell
# 查看磁盘
lsblk
# 挂载硬盘
mount /dev/sdb2 /home/cntd/mnt
# 挂载失败用如下命令
mount -t ntfs-3g /dev/sdb2 /home/cntd/mnt
# 取消挂载
umount /dev/sdb2
# 目标忙
fuser -mv  /home/cntd/user/konglingquan/mnt
kill -9 xxx
```



# 时间相关

```shell
date：查看当前服务器时间
date "+%Y-%m-%d %H:%M:%S" :查看当前时间的格式
date -s "20230726 10:08:00" ：设置当前服务器时间
date "+%j" ：查看几天是今年内的第几天
#=============================================
%S：秒（00~59）
%M：分钟（00~59）
%H：小时（00~23）
%I：小时（00~12）
%m：月份（1~12）
%p：显示出AM或PM
%a：缩写的工作日名称
%A：完整的巩固走日名称
%b：缩写的月份名称
%B：完整的月份名称
%q：季度（1~4）
%y：简写年份
%Y：完整年份
%d：本月的第几天
%j：本年的第几天
%n：换行符
%t：跳格
```



同步时间

```
sudo timedatectl set-timezone Asia/Shanghai
sudo timedatectl set-ntp true

```

