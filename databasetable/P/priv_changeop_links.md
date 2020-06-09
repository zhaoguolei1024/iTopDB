| 列         | 类型                                                    | 注释 |
| :--------- | ------------------------------------------------------- | ---- |
| id         | int                                                     |      |
| item_class | varchar(255) *NULL* []                                  |      |
| item_id    | int *NULL* [**0**]                                      |      |
| optype     | varchar(255) *NULL* [**CMDBChangeOpSetAttributeLinks**] |      |

### 索引

| PRIMARY | *id*         |
| :------ | ------------ |
| INDEX   | *optype*(95) |