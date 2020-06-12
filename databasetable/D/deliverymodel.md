| 列          | 类型                   | 注释 |
| :---------- | ---------------------- | ---- |
| id          | int *自动增量*         |      |
| name        | varchar(255) *NULL* [] |      |
| org_id      | int *NULL* [**0**]     |      |
| description | text *NULL*            |      |

### 索引

| PRIMARY | *id*       |
| :------ | ---------- |
| INDEX   | *name*(95) |
| INDEX   | *org_id*   |