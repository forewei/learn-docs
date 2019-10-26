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

