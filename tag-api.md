TAG-API-DOC
===

## 标签-API-接口文档


### 所属

|项目 |地址 |模块 |访问 |备注 |负责人 |
|---- |:---|:---|:----:|:----:|:----:|
|cloud-api |git@git.acfun.tv:cloud/cloud-api |tag-api |http://api.aixifan.com/tag/tags |api 接口项目/标签 |王志鹏 |


## #TAG

### 接口(v10)

#### 查询标签列表

##### 请求

```
GET http://api.aixifan.com/tag/tags
```

|参数 |说明 |必须/默认值 |备注 |
|---- |:---|:---|:----:|
|page.num |页号 |No/1 |int 限制大小(min>0) |
|page.size |页大小 |No/20 |int 限制大小(min>0) |
|tag.id |标签id |No |int |
|tag.name |标签名称 |No |String |
|tag.groupId |所属标签组 |No |int |
|tag.status |标签状态（1:显示/0:隐藏） |No |int |
|tag.ids |批量标签id |No |integer[] |
##### 示例
```
$ curl -X GET http://api.aixifan.com/tag/tags?page={"num":1,"size":10}&tag={ids:[1,2,3]} \
       -H "Api-Version:v10"
```
```
$ curl -X GET http://api.aixifan.com/tag/tags?page=%7B%22num%22%3A1%2C%22size%22%3A10%7D \
       -H "Api-Version:v10"
```
##### Return 结果
    
```
{
  "total": 5,
  "content": [
    {
      "id": 1,
      "groupId": 1,
      "name": "yule",
      "intro": "yule",
      "type":1,
      "image":"http://img.aixifan.com/tag/1",
      "status":1,
      "createrId": 1,
      "createdAt": "2016-03-26T02:00:00Z"
    },
    ...
  ],
  "num": 1,
  "size": 20,
  "sort": null
}

```

### 接口(v10)

#### 查询标签

##### 请求

```
GET http://api.aixifan.com/tag/tags/{id}
```

|参数 |说明 |必须/默认值 |备注 |
|---- |:---|:---|:----:|
|id |标签的id | Yes |int 限制大小(min>0) |


##### 示例

```
$ curl -X GET http://api.aixifan.com/tag/tags/1 \
       -H "Api-Version:v10"
```
##### Return 结果
    
```
{
  "id": 1,
  "groupId": 1,
  "name": "yule",
  "intro": "yule",
  "type":1,
  "image":"http://img.aixifan.com/tag/1",
  "status":1,
  "createrId": 1,
  "createdAt": "2016-03-26T02:00:00Z"
}	

```

### 接口(v10)

#### 根据名称批量查询标签

##### 请求

```
GET http://api.aixifan.com/tag/tags/names
```

|参数 |说明 |必须/默认值 |备注 |
|---- |:---|:---|:----:|
|names |String，多个名称用“,”隔开 | Yes |String 例如： names=tiyu,视频|


##### 示例

```
$ curl -X GET http://api.aixifan.com/tag/tags/names?names=tiyu,视频 \
       -H "Api-Version:v10"
```
##### Return 结果
    
```
[
  {
    "id": 147188,
    "groupId": 3,
    "name": "tiyu",
    "intro": "",
    "image": "",
    "status": 1,
    "subscriptionCount": 0,
    "contentCount": 0,
    "videoCount": 0,
    "articleCount": 0,
    "albumCount": 0,
    "bangumiCount": 0,
    "createrId": null,
    "createdAt": 1465996960000,
    "updaterId": null,
    "updatedAt": null,
    "deleterId": null,
    "deletedAt": null,
    "relatedTags": null
  },
  {
    "id": 1,
    "groupId": 3,
    "name": "视频",
    "intro": "",
    "image": "",
    "status": 1,
    "subscriptionCount": 0,
    "contentCount": 0,
    "videoCount": 0,
    "articleCount": 0,
    "albumCount": 0,
    "bangumiCount": 0,
    "createrId": null,
    "createdAt": 1465996240000,
    "updaterId": null,
    "updatedAt": null,
    "deleterId": null,
    "deletedAt": null,
    "relatedTags": null
  }
]	

```



### 接口(v10)

#### 添加新标签

##### 请求

```
POST http://api.aixifan.com/tag/tags
```

|参数 |说明 |必须/默认值 |备注 |
|---- |:---|:---|:----:|
| tag.groupId |标签的组Id| Yes | |
| tag.name |标签名称| Yes | |
| tag.intro |标签描述 | Yes | |
| tag.type |标签类型| Yes | 1 普通标签；2 平台标签；3 隐形标签|
| tag.image |标签图| Yes | |
| tag.status |标签状态 | Yes | 0 隐藏；1 显示|
| tag.relatedTags |关联标签 | No | Tag对象数组类型|

##### 示例

```
$ curl -X POST http://api.aixifan.com/tag/tags \
     -H "Api-Version:v10" \
     -H "Content-Type:application/json" \
     -d '{"tag":{"groupId":1,"name":"yule","intro":"yule","type":1,"image":"http://img.aixifan.com/tag/1","status":1,"relatedTags":[{"name":"tiyu"},{"name":"yule"}]}}'
```
##### Return 结果
    
```
{
  "id": 1,
  "groupId": 1,
  "name": "yule",
  "intro": "yule",
  "type":1,
  "image":"http://img.aixifan.com/tag/1",
  "status":1,
  "createrId": 1,
  "createdAt": "2016-03-26T02:00:00Z"
}	

```


### 接口(v10)

#### 【批量】添加新标签

##### 请求

```
POST http://api.aixifan.com/tag/tags/batch
```

|参数 |说明 |必须/默认值 |备注 |
|---- |:---|:---|:----:|
| tags.tag.groupId |标签的组Id| Yes | |
| tags.tag.name |标签名称| Yes | |
| tags.tag.intro |标签描述 | Yes | |
| tags.tag.type |标签类型| Yes | 1 普通标签；2 平台标签；3 隐形标签|
| tags.tag.image |标签图| Yes | |
| tags.tag.status |标签状态 | Yes | 0 隐藏；1 显示|

##### 示例

```
$ curl -X POST http://api.aixifan.com/tag/tags/batch \
     -H "Api-Version:v10" \
     -H "Content-Type:application/json" \
     -d '{"tags":[{"groupId":2,"name":"NBA"},{"groupId":2,"name":"NBA222","intro":"yule","type":1,"image":"http://img.aixifan.com/tag/1","status":1}]}'
```
##### Return 结果
    
```
[
  {
    "id": 1,
    "groupId": 2,
    "name": "NBA222",
    "intro": "yule",
    "type":1,
    "image":"http://img.aixifan.com/tag/1",
    "status":1,
    "createrId": 1,
    "createdAt": "2016-03-26T02:00:00Z"
  } 
]

```


### 接口(v10)

#### 更新标签

##### 请求

```
PUT http://api.aixifan.com/tag/tags/{id}
```

|参数 |说明 |必须/默认值 |备注 |
|---- |:---|:---|:----:|
|id |标签的id | Yes |int 限制大小(min>0) |
| tag.groupId |标签的组Id| No | |
| tag.name |标签名称| No | |
| tag.intro |标签描述 | No | |
| tag.type |标签类型| No | 1 普通标签；2 平台标签；3 隐形标签|
| tag.image |标签图| No | |
| tag.status |标签状态 | No | 0 隐藏；1 显示|

##### 示例

```
$ curl -X PUT http://api.aixifan.com/tag/tags/1 \
       -H "Api-Version:v10" \
       -H "Content-Type:application/json" \
       -d '{"tag":{"name":"tiyu"}}'
```

##### Return 结果

```
{
  "id": 1,
  "groupId": 1,
  "name": "tiyu",
  "intro": "yule",
  "type":1,
  "image":"http://img.aixifan.com/tag/1",
  "status":1,
  "createrId": 1,
  "createdAt": "2016-03-26T02:00:00Z",
  "updaterId": 1,
  "updatedAt": "2016-03-27T02:00:00Z"
}

```


### 接口(v10)

#### 【批量】更新标签

##### 请求

```
PUT http://api.aixifan.com/tag/tags/batch
```

|参数 |说明 |必须/默认值 |备注 |
|---- |:---|:---|:----:|
|id |标签的id | Yes |int 限制大小(min>0) |
| tags.tag.id |标签Id| Yes | |
| tags.tag.groupId |标签的组Id| No | |
| tags.tag.name |标签名称| No | |
| tags.tag.intro |标签描述 | No | |
| tags.tag.type |标签类型| No | 1 普通标签；2 平台标签；3 隐形标签|
| tags.tag.image |标签图| No | |
| tags.tag.status |标签状态 | No | 0 隐藏；1 显示|

##### 示例

```
$ curl -X PUT http://api.aixifan.com/tag/tags/batch \
       -H "Api-Version:v10" \
       -H "Content-Type:application/json" \
       -d '{"tags":[{"id":3,"name":"NBA"},{"id":4,"name":"NBA"}]}'
```

##### Return 结果

```
[
  {
    "id": 3,
    "groupId": 1,
    "name": "NBA",
    "intro": "yule",
    "type": 1,
    "image": "http://img.aixifan.com/tag/1",
    "status": 1,
    "createrId": 1,
    "createdAt": "2016-03-26T02:00:00Z",
    "updaterId": 1,
    "updatedAt": "2016-03-27T02:00:00Z"
  },
  {
    "id": 4,
    "groupId": 1,
    "name": "NBA",
    "intro": "yule",
    "type": 1,
    "image": "http://img.aixifan.com/tag/1",
    "status": 1,
    "createrId": 1,
    "createdAt": "2016-03-26T02:00:00Z",
    "updaterId": 1,
    "updatedAt": "2016-03-27T02:00:00Z"
  }
]

```



### 接口(v10)

#### 删除标签

##### 请求

```
DELETE http://api.aixifan.com/tag/tags/{id}
```

|参数 |说明 |必须/默认值 |备注 |
|---- |:---|:---|:----:|
|id |删除的标签id |Yes |int 限制大小(min>0) |


##### 示例

```
$ curl -X DELETE http://api.aixifan.com/tag/tags/1 \
       -H "Api-Version:v10"
```
##### Return 结果
    
```
true

```

## #GROUP

### 接口(v10)

#### 查询标签组列表

##### 请求

```
GET http://api.aixifan.com/tag/groups
```

|参数 |说明 |必须/默认值 |备注 |
|---- |:---|:---|:----:|
|page.num |页号 |No/1 |int 限制大小(min>0) |
|page.size |页大小 |No/20 |int 限制大小(min>0) |
|group.id |标签组的Id| No | |
|group.pid |父标签组的Id| No | |
|group.name |标签组名称| No | |
|group.status |标签组状态 | No | 0 隐藏；1 显示|
|group.permissionId |标签组权限id | No | |

##### 示例

```
$ curl -X GET http://api.aixifan.com/tag/groups?page=%7B%22num%22%3A1%2C%22size%22%3A10%7D \
       -H "Api-Version:v10"
```
##### Return 结果
    
```
{
  "total": 2,
  "content": [
    {
      "id": 1,
      "name": "group1",
      "intro": "group1",
      "image":"http://img.aixifan.com/group/1",
      "sort":1,
      "status":1,
      "createrId": 1,
      "createdAt": "2016-03-26T02:00:00Z"
    },
    ...
  ],
  "num": 1,
  "size": 20,
  "sort": null
}

```

### 接口(v10)

#### 查询标签组

##### 请求

```
GET http://api.aixifan.com/tag/groups/{id}
```

|参数 |说明 |必须/默认值 |备注 |
|---- |:---|:---|:----:|
|id |标签组的id | Yes |int 限制大小(min>0) |


##### 示例

```
$ curl -X GET http://api.aixifan.com/tag/groups/1 \
       -H "Api-Version:v10"
```
##### Return 结果
    
```
{
  "id": 1,
  "pid": 1,
  "hasChildren": true,
  "name": "group1",
  "intro": "group1",
  "image":"http://img.aixifan.com/group/1",
  "sort":1,
  "status":1,
  "createrId": 1,
  "createdAt": "2016-03-26T02:00:00Z"
}	

```


### 接口(v10)

#### 添加新标签组

##### 请求

```
POST http://api.aixifan.com/tag/groups
```

|参数 |说明 |必须/默认值 |备注 |
|---- |:---|:---|:----:|
| group.pid |标签组的父Id| Yes | |
| group.name |标签组名称| Yes | |
| group.intro |标签组描述 | Yes | |
| group.image |标签组图| Yes | |
| group.sort |标签组排序值| Yes | |
| group.status |标签组状态 | Yes | 0 隐藏；1 显示|

##### 示例

```
$ curl -X POST http://api.aixifan.com/tag/groups \
     -H "Api-Version:v10" \
     -H "Content-Type:application/json" \
     -d '{"group":{"pid":1,"name":"group1","intro":"group1","image":"http://img.aixifan.com/group/1","sort":1,"status":1}}'
```
##### Return 结果
    
```
{
  "id": 1,
  "pid": 1,
  "name": "group1",
  "intro": "group1",
  "image":"http://img.aixifan.com/group/1",
  "sort":1,
  "status":1,
  "createrId": 1,
  "createdAt": "2016-03-26T02:00:00Z"
}

```

### 接口(v10)

#### 更新标签组

##### 请求

```
PUT http://api.aixifan.com/tag/groups/{id}
```

|参数 |说明 |必须/默认值 |备注 |
|---- |:---|:---|:----:|
|id |标签组的id | Yes |int 限制大小(min>0) |
| group.pid |标签组的父Id| No | |
| group.name |标签组名称| No | |
| group.intro |标签组描述 | No | |
| group.image |标签组图| Yes | |
| group.sort |标签组排序值| Yes | |
| group.status |标签组状态 | Yes | 0 隐藏；1 显示|

##### 示例

```
$ curl -X PUT http://api.aixifan.com/tag/groups/1 \
       -H "Api-Version:v10" \
       -H "Content-Type:application/json" \
       -d '{"group":{"name":"group2","intro":"group2"}}'
```

##### Return 结果

```
{
  "id": 1,
  "pid": 1,
  "name": "group2",
  "intro": "group2",
  "image":"http://img.aixifan.com/group/1",
  "sort":1,
  "status":1,
  "createrId": 1,
  "createdAt": "2016-03-26T02:00:00Z",
  "updaterId": 1,
  "updatedAt": "2016-03-27T02:00:00Z"
}

```


### 接口(v10)

#### 批量更新标签组

##### 请求

```
PUT http://api.aixifan.com/tag/groups/{id}
```

|参数 |说明 |必须/默认值 |备注 |
|---- |:---|:---|:----:|
|id |标签组的id | Yes |int 限制大小(min>0) |
| groups.group.pid |标签组的父Id| No | |
| groups.group.name |标签组名称| No | |
| groups.group.intro |标签组描述 | No | |
| groups.group.image |标签组图| Yes | |
| groups.group.sort |标签组排序值| Yes | |
| groups.group.status |标签组状态 | Yes | 0 隐藏；1 显示|

##### 示例

```
$ curl -X PUT http://api.aixifan.com/tag/groups/1 \
       -H "Api-Version:v10" \
       -H "Content-Type:application/json" \
       -d '{"groups":[{"id":1,"name":"group3"},{"id":2,"name":"group3"}]}'
```

##### Return 结果

```
[
  {
    "id": 1,
    "pid": 1,
    "name": "group3",
    "intro": "group2",
    "image": "http://img.aixifan.com/group/1",
    "sort": 1,
    "status": 1,
    "createrId": 1,
    "createdAt": "2016-03-26T02:00:00Z",
    "updaterId": 1,
    "updatedAt": "2016-03-27T02:00:00Z"
  },
  {
    "id": 2,
    "pid": 1,
    "name": "group3",
    "intro": "group2",
    "image": "http://img.aixifan.com/group/1",
    "sort": 1,
    "status": 1,
    "createrId": 1,
    "createdAt": "2016-03-26T02:00:00Z",
    "updaterId": 1,
    "updatedAt": "2016-03-27T02:00:00Z"
  }
]

```



### 接口(v10)

#### 删除标签组

##### 请求

```
DELETE http://api.aixifan.com/tag/groups/{id}
```

|参数 |说明 |必须/默认值 |备注 |
|---- |:---|:---|:----:|
|id |删除的标签组id |Yes |int 限制大小(min>0) |


##### 示例

```
$ curl -X DELETE http://api.aixifan.com/tag/groups/1 \
       -H "Api-Version:v10"
```
##### Return 结果
    
```
true

```
