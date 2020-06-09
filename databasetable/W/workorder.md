| 列          | 类型                                    | 注释 |
| :---------- | --------------------------------------- | ---- |
| id          | int *自动增量*                          |      |
| name        | varchar(255) *NULL* []                  |      |
| status      | enum('closed','open') *NULL* [**open**] |      |
| description | text *NULL*                             |      |
| ticket_id   | int *NULL* [**0**]                      |      |
| team_id     | int *NULL* [**0**]                      |      |
| owner_id    | int *NULL* [**0**]                      |      |
| start_date  | datetime *NULL*                         |      |
| end_date    | datetime *NULL*                         |      |
| log         | longtext *NULL*                         |      |
| log_index   | blob *NULL*                             |      |

### 索引

| PRIMARY | *id*        |
| :------ | ----------- |
| INDEX   | *name*(95)  |
| INDEX   | *ticket_id* |
| INDEX   | *team_id*   |
| INDEX   | *owner_id*  |