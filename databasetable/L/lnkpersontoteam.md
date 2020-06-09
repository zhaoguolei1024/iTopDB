| 列        | 类型               | 注释 |
| :-------- | ------------------ | ---- |
| id        | int *自动增量*     |      |
| team_id   | int *NULL* [**0**] |      |
| person_id | int *NULL* [**0**] |      |
| role_id   | int *NULL* [**0**] |      |

### 索引

| PRIMARY | *id*        |
| :------ | ----------- |
| INDEX   | *team_id*   |
| INDEX   | *person_id* |
| INDEX   | *role_id*   |