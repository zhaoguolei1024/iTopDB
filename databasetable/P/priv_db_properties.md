| 列             | 类型                   | 注释 |
| :------------- | ---------------------- | ---- |
| id             | int *自动增量*         |      |
| name           | varchar(255) *NULL* [] |      |
| description    | varchar(255) *NULL* [] |      |
| value          | varchar(255) *NULL* [] |      |
| change_date    | datetime *NULL*        |      |
| change_comment | varchar(255) *NULL* [] |      |

### 索引

| PRIMARY | *id*       |
| :------ | ---------- |
| INDEX   | *name*(95) |