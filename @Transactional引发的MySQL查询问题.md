# @Transactional引发的MySQL查询问题

使用 `@Transactional` 注解在本方法执行时，当执行完第3行的SQL语句后，此方法的返回值i为1，证明删除成功，这个时候去MySQL查询本条数据时，实际还未进行删除。当使用了注解时，当方法return也就是执行完之后，才会进行数据库更新。

```java
    @Transactional
    public SysResult<String> deleteEnhanceRule(EnhanceRuleDTO enhanceRuleDTO) {
        int i = enhanceRuleMapper.deleteEnhanceRule(enhanceRuleDTO);
        if (i == 0) {
            return SysResult.error("删除失败");
        }
        return SysResult.success();
    }
```
