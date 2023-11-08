# SpringBoot Controller层如何接收指定格式的LocalDateTime参数

在实体类中使用  @JsonFormat 注解：

```java
@JsonFormat(pattern = "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'", timezone = "UTC")
private LocalDateTime createTime;
```