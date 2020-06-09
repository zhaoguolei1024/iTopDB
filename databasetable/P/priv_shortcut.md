| 列        | 类型                               | 注释 |
| :-------- | ---------------------------------- | ---- |
| id        | int *自动增量*                     |      |
| user_id   | int *NULL* [**0**]                 |      |
| name      | varchar(255) *NULL* []             |      |
| context   | text *NULL*                        |      |
| realclass | varchar(255) *NULL* [**Shortcut**] |      |

### 索引

| PRIMARY | *id*            |
| :------ | --------------- |
| INDEX   | *user_id*       |
| INDEX   | *name*(95)      |
| INDEX   | *realclass*(95) |