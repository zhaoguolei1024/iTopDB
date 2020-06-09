| 列          | 类型                            | 注释 |
| :---------- | ------------------------------- | ---- |
| id          | int *自动增量*                  |      |
| name        | varchar(255) *NULL* []          |      |
| description | text *NULL*                     |      |
| realclass   | varchar(255) *NULL* [**Query**] |      |

### 索引

| PRIMARY | *id*            |
| :------ | --------------- |
| INDEX   | *name*(95)      |
| INDEX   | *realclass*(95) |