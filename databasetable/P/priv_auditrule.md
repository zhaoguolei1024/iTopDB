| 列          | 类型                                   | 注释 |
| :---------- | -------------------------------------- | ---- |
| id          | int *自动增量*                         |      |
| name        | varchar(255) *NULL* []                 |      |
| description | varchar(255) *NULL* []                 |      |
| query       | text *NULL*                            |      |
| valid_flag  | enum('false','true') *NULL* [**true**] |      |
| category_id | int *NULL* [**0**]                     |      |

### 索引

| PRIMARY | *id*          |
| :------ | ------------- |
| INDEX   | *name*(95)    |
| INDEX   | *category_id* |