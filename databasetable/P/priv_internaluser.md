| 列                   | 类型                                   | 注释 |
| :------------------- | -------------------------------------- | ---- |
| id                   | int *自动增量*                         |      |
| reset_pwd_token_hash | tinyblob *NULL*                        |      |
| reset_pwd_token_salt | tinyblob *NULL*                        |      |
| finalclass           | varchar(255) *NULL* [**UserInternal**] |      |

### 索引

| PRIMARY | *id*             |
| :------ | ---------------- |
| INDEX   | *finalclass*(95) |