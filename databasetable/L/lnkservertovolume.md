| 列        | 类型                   | 注释 |
| :-------- | ---------------------- | ---- |
| id        | int *自动增量*         |      |
| volume_id | int *NULL* [**0**]     |      |
| server_id | int *NULL* [**0**]     |      |
| size_used | varchar(255) *NULL* [] |      |

### 索引

| PRIMARY | *id*        |
| :------ | ----------- |
| INDEX   | *volume_id* |
| INDEX   | *server_id* |