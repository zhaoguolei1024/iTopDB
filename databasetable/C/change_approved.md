| 列               | 类型                                     | 注释 |
| :--------------- | ---------------------------------------- | ---- |
| id               | int *自动增量*                           |      |
| approval_date    | datetime *NULL*                          |      |
| approval_comment | varchar(255) *NULL* []                   |      |
| finalclass       | varchar(255) *NULL* [**ApprovedChange**] |      |

### 索引

| PRIMARY | *id*             |
| :------ | ---------------- |
| INDEX   | *finalclass*(95) |