ticket

工单 (Ticket)



| 列                 | 类型                                                     | 注释                                                         |
| :----------------- | -------------------------------------------------------- | ------------------------------------------------------------ |
| id                 | int *自动增量*                                           | 自增ID                                                       |
| operational_status | enum('closed','ongoing','resolved') *NULL* [**ongoing**] | 操作状态，进行中 (ongoing), 已解决 (resolved), 已关闭 (closed) |
| ref                | varchar(255) *NULL* []                                   | 编号                                                         |
| org_id             | int *NULL* [**0**]                                       | 组织ID                                                       |
| caller_id          | int *NULL* [**0**]                                       | 发起人，personid                                             |
| team_id            | int *NULL* [**0**]                                       | 执行团队,teamid                                              |
| agent_id           | int *NULL* [**0**]                                       | 办理人,personid                                              |
| title              | varchar(255) *NULL* []                                   | 标题                                                         |
| description        | text *NULL*                                              | 描述                                                         |
| description_format | enum('text','html') *NULL* [**text**]                    | 描述格式,text,html                                           |
| start_date         | datetime *NULL*                                          | 开始日期                                                     |
| end_date           | datetime *NULL*                                          | 结束日期                                                     |
| last_update        | datetime *NULL*                                          | 最后更新                                                     |
| close_date         | datetime *NULL*                                          | 关闭日期                                                     |
| private_log        | longtext *NULL*                                          | 私信                                                         |
| private_log_index  | blob *NULL*                                              | 私信顺序                                                     |
| finalclass         | varchar(255) *NULL* [**Ticket**]                         | 类型                                                         |

### 索引

| PRIMARY | *id*                 |
| :------ | -------------------- |
| INDEX   | *operational_status* |
| INDEX   | *ref*(95)            |
| INDEX   | *org_id*             |
| INDEX   | *caller_id*          |
| INDEX   | *team_id*            |
| INDEX   | *agent_id*           |
| INDEX   | *finalclass*(95)     |