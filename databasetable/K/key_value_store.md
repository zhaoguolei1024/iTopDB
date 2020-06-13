key_value_store





| 列        | 类型                        | 注释 |
| :-------- | --------------------------- | ---- |
| id        | int *自动增量*              |      |
| namespace | varchar(255) *NULL* []      |      |
| key_name  | varchar(255) *NULL* []      |      |
| value     | varchar(255) *NULL* [**0**] |      |

### 索引

| PRIMARY | *id*                            |
| :------ | ------------------------------- |
| INDEX   | *key_name*(95)                  |
| INDEX   | *key_name*(95), *namespace*(95) |