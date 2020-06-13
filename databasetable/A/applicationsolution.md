## applicationsolution

## 应用方案

配置管理--配置项--应用方案

功能配置项 (FunctionalCI) >> ApplicationSolution



| 列         | 类型                                          | 注释                                 |
| :--------- | --------------------------------------------- | ------------------------------------ |
| id         | int *自动增量*                                | 关联FunctionalCI数据表的ID           |
| status     | enum('active','inactive') *NULL* [**active**] | 状态，启用 (active), 停用 (inactive) |
| redundancy | varchar(20) *NULL* [**disabled**]             | 冗余配置                             |

### 索引

| PRIMARY | *id* |
| :------ | ---- |
|         |      |