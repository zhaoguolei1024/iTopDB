change_approved

已变更的批准

| 列               | 类型                                     | 注释     |
| :--------------- | ---------------------------------------- | -------- |
| id               | int *自动增量*                           | 自增ID   |
| approval_date    | datetime *NULL*                          | 批准日期 |
| approval_comment | varchar(255) *NULL* []                   | 批准说明 |
| finalclass       | varchar(255) *NULL* [**ApprovedChange**] | 类型     |

### 索引

| PRIMARY | *id*             |
| :------ | ---------------- |
| INDEX   | *finalclass*(95) |

