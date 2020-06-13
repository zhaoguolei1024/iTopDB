priv_changeop_links

CMDBChangeOpSetAttributeLinks (CMDBChangeOpSetAttributeLinks)

变更操作 (CMDBChangeOp) >> 对象变化 (CMDBChangeOpSetAttribute) >> CMDBChangeOpSetAttributeLinks



| 列         | 类型                                                    | 注释     |
| :--------- | ------------------------------------------------------- | -------- |
| id         | int                                                     | 自增ID   |
| item_class | varchar(255) *NULL* []                                  | 项目类别 |
| item_id    | int *NULL* [**0**]                                      | 项目ID   |
| optype     | varchar(255) *NULL* [**CMDBChangeOpSetAttributeLinks**] | 操作类型 |

### 索引

| PRIMARY | *id*         |
| :------ | ------------ |
| INDEX   | *optype*(95) |