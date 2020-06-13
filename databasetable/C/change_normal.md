change_normal

工单 (Ticket) >> 变更 (Change) >> 已批准的变更 (ApprovedChange) >> NormalChange

正常变更

| 列                 | 类型            | 注释     |
| :----------------- | --------------- | -------- |
| id                 | int *自动增量*  | 自增ID   |
| acceptance_date    | datetime *NULL* | 审核日期 |
| acceptance_comment | text *NULL*     | 审核说明 |

### 索引

| PRIMARY | *id* |
| :------ | ---- |
|         |      |