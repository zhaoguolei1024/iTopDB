| 列        | 类型                                           | 注释 |
| :-------- | ---------------------------------------------- | ---- |
| id        | int *自动增量*                                 |      |
| state     | varchar(255) *NULL* []                         |      |
| realclass | varchar(255) *NULL* [**TriggerOnStateChange**] |      |

### 索引

| PRIMARY | *id*            |
| :------ | --------------- |
| INDEX   | *realclass*(95) |