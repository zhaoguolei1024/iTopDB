| 列        | 类型                            | 注释 |
| :-------- | ------------------------------- | ---- |
| id        | int *自动增量*                  |      |
| message   | text *NULL*                     |      |
| date      | datetime *NULL*                 |      |
| userinfo  | varchar(255) *NULL* []          |      |
| realclass | varchar(255) *NULL* [**Event**] |      |

### 索引

| PRIMARY | *id*            |
| :------ | --------------- |
| INDEX   | *realclass*(95) |