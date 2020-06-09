## applicationsolution

## 应用方案

配置管理--配置项--应用方案



| 列         | 类型                                          | 注释                                   |
| :--------- | --------------------------------------------- | -------------------------------------- |
| id         | int *自动增量*                                | 关联FunctionalCI数据表的ID             |
| status     | enum('active','inactive') *NULL* [**active**] | 是否启用，启用为active，禁用为inactive |
| redundancy | varchar(20) *NULL* [**disabled**]             | 冗余配置                               |

### 索引

| PRIMARY | *id* |
| :------ | ---- |
|         |      |