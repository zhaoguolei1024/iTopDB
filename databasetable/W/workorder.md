workorder

工作任务 (WorkOrder)





| 列          | 类型                                    | 注释                               |
| :---------- | --------------------------------------- | ---------------------------------- |
| id          | int *自动增量*                          | 自增ID                             |
| name        | varchar(255) *NULL* []                  | 名称                               |
| status      | enum('closed','open') *NULL* [**open**] | 状态，已关闭 (closed), 打开 (open) |
| description | text *NULL*                             | 描述                               |
| ticket_id   | int *NULL* [**0**]                      | 工单ID                             |
| team_id     | int *NULL* [**0**]                      | 执行团队ID                         |
| owner_id    | int *NULL* [**0**]                      | 办理人 (agent_id)                  |
| start_date  | datetime *NULL*                         | 开始日期                           |
| end_date    | datetime *NULL*                         | 结束日期                           |
| log         | longtext *NULL*                         | 日志                               |
| log_index   | blob *NULL*                             | 日志顺序                           |

### 索引

| PRIMARY | *id*        |
| :------ | ----------- |
| INDEX   | *name*(95)  |
| INDEX   | *ticket_id* |
| INDEX   | *team_id*   |
| INDEX   | *owner_id*  |