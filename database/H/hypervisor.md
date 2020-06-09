| 列        | 类型               | 注释 |
| :-------- | ------------------ | ---- |
| id        | int *自动增量*     |      |
| farm_id   | int *NULL* [**0**] |      |
| server_id | int *NULL* [**0**] |      |

### 索引

| PRIMARY | *id*        |
| :------ | ----------- |
| INDEX   | *farm_id*   |
| INDEX   | *server_id* |