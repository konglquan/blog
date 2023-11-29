# IDEA解决控制台乱码问题

![image-20231129102702826](imgs/image-20231129102702826.png)



![image-20231129102721897](imgs/image-20231129102721897.png)



位置：Help -> Edit Custom VM Options...

如图增加下面一行后，重启idea即可

```
-Dfile.encoding=UTF-8
```

