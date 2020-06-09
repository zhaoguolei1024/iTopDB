| 列      | 类型                                               | 注释 |
| :------ | -------------------------------------------------- | ---- |
| id      | int                                                |      |
| attcode | varchar(255) *NULL* []                             |      |
| optype  | varchar(255) *NULL* [**CMDBChangeOpSetAttribute**] |      |

### 索引

| PRIMARY | *id*         |
| :------ | ------------ |
| INDEX   | *optype*(95) |