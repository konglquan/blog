# Mybatis的XML中判空问题!=''

报错信息如下

```java
Caused by: com.fasterxml.jackson.databind.exc.InvalidFormatException: Cannot deserialize value of type `java.time.LocalDateTime` from String "2023-10-01 00:00:00": Failed to deserialize java.time.LocalDateTime: (java.time.format.DateTimeParseException) Text '2023-10-01 00:00:00' could not be parsed at index 10
 at [Source: (org.springframework.util.StreamUtils$NonClosingInputStream); line: 2, column: 23] (through reference chain: cn.ac.ist.filter.vo.EnhanceRuleVo["createTimeStart"])

```

问题代码：

```xml
<if test="enhanceRuleVo.createTimeStart != null and enhanceRuleVo.createTimeStart !=''">
    and create_time &gt;= #{enhanceRuleVo.createTimeStart}
</if>
```

解决办法：

```xml
<if test="enhanceRuleVo.createTimeStart != null">
  	and create_time &gt;= #{enhanceRuleVo.createTimeStart}
</if>
```

Boolean类型也会出现类似的问题

```xml
<if test="enhanceRuleVo.isSystem != null">
   and is_system = #{enhanceRuleVo.isSystem}
</if>
```

