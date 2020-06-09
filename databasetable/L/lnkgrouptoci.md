| 列       | 类型                   | 注释 |
| :------- | ---------------------- | ---- |
| id       | int *自动增量*         |      |
| group_id | int *NULL* [**0**]     |      |
| ci_id    | int *NULL* [**0**]     |      |
| reason   | varchar(255) *NULL* [] |      |

### 索引

| PRIMARY | *id*       |
| :------ | ---------- |
| INDEX   | *group_id* |
| INDEX   | *ci_id*    |