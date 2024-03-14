# 安装





## Linux安装ElasticSearch





## Windows安装ElasticSearch



# 命令

## 启动ElasticSearch

```shell
# 1、进入bin目录，切换到es用户
cd ./bin
su es
# 2、启动ElasticSearch
./elasticsearch -d
# 3、查看ElasticSearch状态
jps -l
ps -ef | grep elastic
```

## 索引

### 查看所有索引

```shell
curl -XGET -u 'user:password' http://localhost:9200/_cat/indices?v
```

### 查看索引数据

```shell
curl -XGET -u 'user:password' http://localhost:9200/indexName/_search?pretty
```

### 根据ID查询

```shell
curl -XGET -u 'user:password'http://localhost:9200//index/_doc/id
```

### 查看索引mapping

```shell
curl -XGET -u 'user:password' http://localhost:9200/indexName/_mapping
```

### 创建索引

```shell
curl -XPUT -u user:password -H 'Content-Type: application/json' http://localhost:9200/indexName -d ''
```

### 刷新索引

```shell
curl -XGET -u 'user:password' http://localhost:9200/indexName/_refresh
```

### 删除索引

```shell
curl -XDELETE  -u 'user:password' http://localhost:9200/indexName
```



## 文档

## 模板

### 查看所有模板

### 新建模板

```shell
curl -XPUT -u 'user:password' -H 'Content-Type: application/json' http://172.31.1.40:9200/_template/cntd_data_dns -d '{"order":0,"template":"cntd_data_dns_*","mappings":{"properties":{"domain":{"type":"keyword","ignore_above":256},"return_ip":{"type":"keyword","ignore_above":256},"time":{"type":"date","store":true,"format":"yyyy-MM-dd HH:mm:ss"},"top_domain":{"type":"keyword","ignore_above":256}}},"settings":{"index":{"number_of_shards":"8","number_of_replicas":"0"}}}'

```

```shell
curl -XPUT -u 'user:password' -H 'Content-Type: application/json' http://172.31.1.40:9200/_template/cntd_data_dns -d '{"order":0,"index_patterns":["cntdddddddtest*"],"settings":{"index":{"number_of_shards":"8","number_of_replicas":"0"}},"mappings":{"properties":{"top_domain":{"ignore_above":256,"type":"keyword"},"return_ip":{"ignore_above":256,"type":"keyword"},"domain":{"ignore_above":256,"type":"keyword"},"time":{"format":"yyyy-MM-dd HH:mm:ss","store":true,"type":"date"}}}}'

```



### 删除模板

## 其他命令

### 刷新分片

```shell
curl -u user:password -XPOST 'http://ip:port/_cluster/reroute?retry_failed=true'
```

## task

### 查看任务

```shell
curl -XGET -u 'user:password' http://ip:port/_cat/tasks?detailed=true&vPOST
```

### 清除任务

### 无法入库（磁盘满了）

1、关闭索引的只读状态：

```shell
curl -XPUT -u 'user:password' -H 'Content-Type: application/json' http://localhost:9200/_all/_settings -d '{"index.blocks.read_only_allow_delete":null}'
```

2、关闭磁盘分配保护

```shell
curl -XPUT -u 'user:password' -H 'Content-Type: application/json' http://localhost:9200/_cluster/settings -d '{"transient":{"cluster.routing.allocation.disk.threshold_enabled":false}}'
```

3、扩容

4、打开磁盘分配保护

```shell
curl -XPUT -u 'user:password' -H 'Content-Type: application/json' http://localhost:9200/_cluster/settings -d '{"transient":{"cluster.routing.allocation.disk.threshold_enabled":false}}'
```

### ES将某个字段插入到整个索引中

```
POST /sc_target_task/_update_by_query

{
  "script": {
    "source": "ctx._source.reportingLevels = params.reportingLevels",
    "params": {
      "reportingLevels": [
        "高危",
        "中危",
        "低危"
      ]
    }
  }
}
```



# 查询API

## java操作es之各种高级查询

```
https://blog.csdn.net/qq_34344432/article/details/122680577
```

