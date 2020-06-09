| 列       | 类型                                   | 注释 |
| :------- | -------------------------------------- | ---- |
| id       | int *自动增量*                         |      |
| changeid | int *NULL* [**0**]                     |      |
| objclass | varchar(255) *NULL* []                 |      |
| objkey   | int *NULL* [**0**]                     |      |
| optype   | varchar(255) *NULL* [**CMDBChangeOp**] |      |

### 索引

| PRIMARY | *id*                     |
| :------ | ------------------------ |
| INDEX   | *changeid*               |
| INDEX   | *optype*(95)             |
| INDEX   | *objclass*(95), *objkey* |