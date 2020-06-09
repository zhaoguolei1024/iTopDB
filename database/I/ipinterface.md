| 列         | 类型                                  | 注释 |
| :--------- | ------------------------------------- | ---- |
| id         | int *自动增量*                        |      |
| ipaddress  | varchar(255) *NULL* []                |      |
| macaddress | varchar(255) *NULL* []                |      |
| comment    | text *NULL*                           |      |
| ipgateway  | varchar(255) *NULL* []                |      |
| ipmask     | varchar(255) *NULL* []                |      |
| speed      | decimal(12,2) *NULL*                  |      |
| finalclass | varchar(255) *NULL* [**IPInterface**] |      |

### 索引

| PRIMARY | *id*             |
| :------ | ---------------- |
| INDEX   | *finalclass*(95) |