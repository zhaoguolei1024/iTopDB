| 列             | 类型                   | 注释 |
| :------------- | ---------------------- | ---- |
| id             | int *自动增量*         |      |
| name           | varchar(255) *NULL* [] |      |
| description    | varchar(255) *NULL* [] |      |
| definition_set | text *NULL*            |      |

### 索引

| PRIMARY | *id*       |
| :------ | ---------- |
| INDEX   | *name*(95) |