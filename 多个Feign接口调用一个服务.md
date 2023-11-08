# 多个Feign接口调用一个服务

### 遇到的问题

> 报错：
>
> The bean ‘xxx.xxxxx’ could not be registered. A bean wirh that name has waleady been defined and oerriding is disable.

原因：在同于一个微服务中多个feign接口使用@FeignClient注解调用同一个名称的微服务，启动时引发的异常

### 解决方法

1、将调用同一服务的Feign接口合并

2、在配置文件中添加如下配置

```yaml
spring:
   main:
      allow-bean-definition-overriding: true
```

注：这个配置是给谁调用feign就谁添加，哪一个服务启动时报这个错就给谁添加

3、在@FeignClient注解上添加contextId属性，确保每个@FeignClient的contextId唯一

```java
// value代表服务名称，contextId这个FeignClient的唯一标识
// 在默认情况下这个值是不变的，所以当有多个fign调用同一个服务是就会报错
@Feignclient(value = "data" , contextId = "employeeRequest")
```

原文：https://blog.csdn.net/weixin_62321552/article/details/125530866