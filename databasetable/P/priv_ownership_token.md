priv_ownership_token

iTopOwnershipToken (iTopOwnershipToken)



| 列        | 类型                   | 注释         |
| :-------- | ---------------------- | ------------ |
| id        | int *自动增量*         | 自增ID       |
| acquired  | datetime *NULL*        | 获取时间     |
| last_seen | datetime *NULL*        | 最后访问时间 |
| obj_class | varchar(255) *NULL* [] | 对象类       |
| obj_key   | int *NULL*             | 对象         |
| token     | varchar(255) *NULL* [] | token        |
| user_id   | int *NULL* [**0**]     | 用户账户     |

### 索引

| PRIMARY | *id*            |
| :------ | --------------- |
| INDEX   | *obj_class*(95) |
| INDEX   | *obj_key*       |
| INDEX   | *user_id*       |