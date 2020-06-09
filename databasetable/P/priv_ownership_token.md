| 列        | 类型                   | 注释 |
| :-------- | ---------------------- | ---- |
| id        | int *自动增量*         |      |
| acquired  | datetime *NULL*        |      |
| last_seen | datetime *NULL*        |      |
| obj_class | varchar(255) *NULL* [] |      |
| obj_key   | int *NULL*             |      |
| token     | varchar(255) *NULL* [] |      |
| user_id   | int *NULL* [**0**]     |      |

### 索引

| PRIMARY | *id*            |
| :------ | --------------- |
| INDEX   | *obj_class*(95) |
| INDEX   | *obj_key*       |
| INDEX   | *user_id*       |