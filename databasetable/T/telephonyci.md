| 列          | 类型                                  | 注释 |
| :---------- | ------------------------------------- | ---- |
| id          | int *自动增量*                        |      |
| phonenumber | varchar(255) *NULL* []                |      |
| finalclass  | varchar(255) *NULL* [**TelephonyCI**] |      |

### 索引

| PRIMARY | *id*             |
| :------ | ---------------- |
| INDEX   | *finalclass*(95) |