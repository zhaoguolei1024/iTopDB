ticket_problem

问题 (Problem)

工单 (Ticket) >> Problem



| 列                    | 类型                                                        | 注释                                                         |
| :-------------------- | ----------------------------------------------------------- | ------------------------------------------------------------ |
| id                    | int *自动增量*                                              | 自增ID                                                       |
| status                | enum('assigned','closed','new','resolved') *NULL* [**new**] | 状态，已分配 (assigned), 已关闭 (closed), 新建 (new), 已解决 (resolved) |
| service_id            | int *NULL* [**0**]                                          | 服务ID                                                       |
| servicesubcategory_id | int *NULL* [**0**]                                          | 子服务ID                                                     |
| product               | varchar(255) *NULL* []                                      | 产品                                                         |
| impact                | enum('1','2','3') *NULL* [**1**]                            | 影响范围，部门 (1), 服务 (2), 个体 (3)                       |
| urgency               | enum('1','2','3','4') *NULL* [**1**]                        | 紧急度，非常高 (1), 高 (2), 中 (3), 低 (4)                   |
| priority              | enum('1','2','3','4') *NULL* [**1**]                        | 优先级，非常高 (1), 高 (2), 中 (3), 低 (4)                   |
| related_change_id     | int *NULL* [**0**]                                          | 相关变更                                                     |
| assignment_date       | datetime *NULL*                                             | 分配日期                                                     |
| resolution_date       | datetime *NULL*                                             | 解决日期                                                     |

### 索引

| PRIMARY | *id*                    |
| :------ | ----------------------- |
| INDEX   | *service_id*            |
| INDEX   | *servicesubcategory_id* |
| INDEX   | *related_change_id*     |