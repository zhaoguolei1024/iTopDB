| 列      | 类型                                                         | 注释 |
| :------ | ------------------------------------------------------------ | ---- |
| id      | int *自动增量*                                               |      |
| name    | varchar(255) *NULL* []                                       |      |
| vendor  | varchar(255) *NULL* []                                       |      |
| version | varchar(255) *NULL* []                                       |      |
| type    | enum('DBServer','Middleware','OtherSoftware','PCSoftware','WebServer') *NULL* |      |

### 索引

| PRIMARY | *id*          |
| :------ | ------------- |
| INDEX   | *name*(95)    |
| INDEX   | *version*(95) |