| 列        | 类型                   | 注释 |
| :-------- | ---------------------- | ---- |
| id        | int *自动增量*         |      |
| user_id   | int *NULL* [**0**]     |      |
| menu_code | varchar(255) *NULL* [] |      |
| contents  | text *NULL*            |      |

### 索引

| PRIMARY | *id*      |
| :------ | --------- |
| INDEX   | *user_id* |