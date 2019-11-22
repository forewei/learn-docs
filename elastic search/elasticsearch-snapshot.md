##  ES 快照备份索引

###    设置备份索引目录

​       进入es安装目录下面的config，编辑elasticsearch.yml加入

```
 path.repo:  /data/elasticsearch/backup
```

###   创建仓库  

```
PUT /_snapshot/my_backup
{
  "type": "fs",
  "settings": {
        "compress":"true",
        "location":"/data/elasticsearch/backup"
  }
}
```

###    查看仓库信息

```
GET /_snapshot/my_backup
```

###  创建备份 

```
PUT /_snapshot/my_backup/snapshot_1?wait_for_completion=true
```

### 指定索引备份

```
PUT /_snapshot/my_backup/snapshot_1
 {
  "indices": "index_cs",
  "ignore_unavailable": "true",
  "include_global_state": false
}
```

### 恢复备份

```
POST /_snapshot/my_backup/snapshot_1/_restore
```

###  查看恢复信息 

```
GET /_recovery?pretty&human
```

es集群需要装nfs挂载到一个中间服务器进行创建snapshot快照