priv_changeop

变更操作 (CMDBChangeOp) - 变更操作跟踪

CMDBChangeOp

| 列       | 类型                                   | 注释       |
| :------- | -------------------------------------- | ---------- |
| id       | int *自动增量*                         | 自增ID     |
| changeid | int *NULL* [**0**]                     | 变更ID     |
| objclass | varchar(255) *NULL* []                 | 对象的类别 |
| objkey   | int *NULL* [**0**]                     | 对象id     |
| optype   | varchar(255) *NULL* [**CMDBChangeOp**] | 对象类型   |

### 索引

| PRIMARY | *id*                     |
| :------ | ------------------------ |
| INDEX   | *changeid*               |
| INDEX   | *optype*(95)             |
| INDEX   | *objclass*(95), *objkey* |