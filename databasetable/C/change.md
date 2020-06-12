## change

变更


| 列                  | 类型                                                         | 注释                                                         |
| :------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| id                  | int *自动增量*                                               | 自增ID                                                       |
| status              | enum('approved','assigned','closed','implemented','monitored','new','notapproved','plannedscheduled','rejected','validated') *NULL* [**new**] | 状态；已批准 (approved), 已分配 (assigned), 已关闭 (closed), 已实施 (implemented), 已验收 (monitored), 新建 (new), 未批准 (notapproved), 已计划和安排 (plannedscheduled), 已驳回 (rejected), 已确认 (validated) |
| reason              | varchar(255) *NULL* []                                       | 驳回原因                                                     |
| requestor_id        | int *NULL* [**0**]                                           | 发起人                                                       |
| creation_date       | datetime *NULL*                                              | 创建时间                                                     |
| impact              | varchar(255) *NULL* []                                       | 影响                                                         |
| supervisor_group_id | int *NULL* [**0**]                                           | 监督团队                                                     |
| supervisor_id       | int *NULL* [**0**]                                           | 监督人                                                       |
| manager_group_id    | int *NULL* [**0**]                                           | 管理团队                                                     |
| manager_id          | int *NULL* [**0**]                                           | 经理                                                         |
| outage              | enum('no','yes') *NULL* [**no**]                             | 停机；否 (no), 是 (yes)                                      |
| fallback            | text *NULL*                                                  | 回滚计划                                                     |
| parent_id           | int *NULL* [**0**]                                           | 父级变更                                                     |
| finalclass          | varchar(255) *NULL* [**Change**]                             | 类型                                                         |

### 索引

| PRIMARY | *id*                  |
| :------ | --------------------- |
| INDEX   | *requestor_id*        |
| INDEX   | *supervisor_group_id* |
| INDEX   | *supervisor_id*       |
| INDEX   | *manager_group_id*    |
| INDEX   | *manager_id*          |
| INDEX   | *parent_id*           |
| INDEX   | *finalclass*(95)      |