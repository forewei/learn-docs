## ElasticSearch 学习笔记

#### 索引操作

##### 创建索引

put   {{ip}}:{{host}}/{{index_name}}

```json
{
	"settings": {
		"index": {
			"number_of_shards": "5",
			"number_of_replicas": "1",
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

##### 查询索引

