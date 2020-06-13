priv_changeop_setatt

对象变化 (CMDBChangeOpSetAttribute) - 对象属性变化跟踪

变更操作 (CMDBChangeOp) >> CMDBChangeOpSetAttribute



| 列      | 类型                                               | 注释     |
| :------ | -------------------------------------------------- | -------- |
| id      | int                                                | ID       |
| attcode | varchar(255) *NULL* []                             | 属性     |
| optype  | varchar(255) *NULL* [**CMDBChangeOpSetAttribute**] | 操作类型 |

### 索引

| PRIMARY | *id*         |
| :------ | ------------ |
| INDEX   | *optype*(95) |