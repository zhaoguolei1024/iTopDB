| 列        | 类型                   | 注释 |
| :-------- | ---------------------- | ---- |
| id        | int *自动增量*         |      |
| name      | varchar(255) *NULL* [] |      |
| version   | varchar(255) *NULL* [] |      |
| installed | datetime *NULL*        |      |
| comment   | text *NULL*            |      |
| parent_id | int *NULL* [**0**]     |      |

### 索引

| PRIMARY | *id*        |
| :------ | ----------- |
| INDEX   | *parent_id* |