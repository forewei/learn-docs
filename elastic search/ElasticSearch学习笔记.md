## ElasticSearch 学习笔记

注 ：所有的请求之前都要加  {ip}:{host}

#### 索引操作（index）

##### 创建索引

PUT  /{index}

```json
{
	"settings": {
		"index": {
			"number_of_shards": "5",  // 分片为5
			"number_of_replicas": "1", //每个分片1个副本
			"analysis": {
				"analyzer": {
					"default": {
						"type": "ik_max_word"  //默认的分词器
					}
				}
			}
		}
	}
}
```



##### 删除索引

DELETE   /{index}

##### 查询索引

GET   /{index}

##### 索引是否存在

HEAD  /{index}

##### 关闭索引

POST   /{index}/_close

POST   /{index}/_open

 open和close索引api允许关闭一个索引，然后再打开它。一个关闭的索引在集群上几乎没有开销(除了维护它的元数据之外)，并且对于读/写操作被阻塞。一个关闭的索引可以被打开，然后进行正常的恢复过程。 

##### 设置索引映射

PUT  /{index}/_mapping/ _doc

允许您向现有索引添加字段，或仅更改现有字段的搜索设置。

##### 查询索引映射

GET /{index}/_mapping/ _doc

##### 索引查询超过10000限制

PUT {index}/_settings?preserve_existing=true

```
{
"max_result_window" : "2000000000"
}
```

##### 索引轮转

##### 创建索引模板

对logs*匹配到的索引都用以下配置

PUT _template/template_logs

```
{
  "template": "logs*",
  "settings": {
    "index": {
      "number_of_shards": "5",
      "number_of_replicas": "1",
      "analysis": {
        "analyzer": {
          "default": {
            "type": "ik_max_word"
          }
        }
      }
    }
  }
}
```

##### 查看索引模板

GET /_teamplate/teamplate_logs

##### 删除索引模板

DELETE /_teamplate/teamplate_logs

##### 修改索引模板

POST /_teamplate/teamplate_logs

```
{
  "template": "logs*",
  "settings": {
    "index": {
      "number_of_shards": "10",
      "number_of_replicas": "1",
      "analysis": {
        "analyzer": {
          "default": {
            "type": "ik_max_word"
          }
        }
      }
    }
  }
}
```

##### 重建索引

把老索引复制到新索引里

POST _reindex

```
{
  "source": {
    "index": "logs-operat-2019-11"
  },
  "dest": {
    "index": "logs-operat-2019.11"
  }
}
```



#### 查询操作

##### match查询

 匹配查询接受文本/数字/日期，分析它们，并构造一个查询。例如: 

GET /{index}/_search

```console
{
    "query": {
        "match" : {
            "message" : "this is a test"
        }
    }
}
```

