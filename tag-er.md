TAG-ER-DOC
===

## 标签-ER-文档


### 所属

|项目 |地址 |模块 |访问 |备注 |负责人 |
|---- |:---|:---|:----:|:----:|:----:|
|cloud-api |git@git.acfun.tv:cloud/cloud-api |tag-api |http://api.aixifan.com/tag/tags |api 接口项目/标签 |王志鹏 |

### 数据结构

#### tag_tag: 标签

|字段名 |类型 |注释 |
|---- |:----|:----|
|id   |Integer |主键	|
|group_id   |Integer |外键：所属标签组Id	  |
|name   |String |标签名称	  |
|intro   |String |标签描述	  |
|type   |Integer |标签类型: 1 普通标签；2 平台标签；3 隐形标签|
|image   |String |标签图	  |
|status   |Integer |标签状态: 0 隐藏；1 显示|
|subscriptionCount   |Integer |订阅数	  |
|contentCount   |Integer |标签下内容总数: 视频数＋文章数＋合辑数＋番剧数|
|videoCount   |Integer |标签下视频总数	  |
|articleCount   |Integer |标签下文章总数	  |
|albumCount   |Integer |标签下合辑总数	  |
|bangumiCount   |Integer |标签下番剧总数	  |
|creater_id   |Integer |创建者Id	  |
|created_at   |Date |创建时间	  |
|updater_id   |Integer |更新者Id	  |
|updated_at   |Date |更新时间	  |
|deleter_id   |Integer |删除者Id	  |
|deleted_at   |Date |删除时间	  |
|ids   |Integer[] |非映射属性，批量标签	  |
|groupIds   |Integer[] |非映射属性，批量标签的组id	  |

#### tag_group: 标签组

|字段名 |类型 |注释 |
|---- |:----|:----|
|id   |Integer |主键	|
|permission_id   |Integer |数据权限Id	|
|pid   |Integer |父标签组Id	|
|has_children   |Integer |是否有子标签组：1 有; 0 没有	|
|name   |String |标签组名称	  |
|intro   |String |标签组描述	  |
|image   |String |标签组图	  |
|sort   |Integer |标签组排序值	  |
|status   |Integer |标签组状态: 0 隐藏；1 显示|
|creater_id   |Integer |创建者Id	  |
|created_at   |Date |创建时间	  |
|updater_id   |Integer |更新者Id	  |
|updated_at   |Date |更新时间	  |
|deleter_id   |Integer |删除者Id	  |
|deleted_at   |Date |删除时间	  |


#### tag_related: 标签关联关系

|字段名 |类型 |注释 |
|---- |:----|:----|
|id   |Integer |主键	|
|tag_id   |Integer |外键：标签Id	  |
|related_tag_id   |Integer |外键：关联标签Id|
