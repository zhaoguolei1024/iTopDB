priv_changeop_setatt_longtext

文本变更跟踪 (CMDBChangeOpSetAttributeText) - 文本变更跟踪

变更操作 (CMDBChangeOp) >> 对象变化 (CMDBChangeOpSetAttribute) >> CMDBChangeOpSetAttributeText



| 列       | 类型                                                       | 注释     |
| :------- | ---------------------------------------------------------- | -------- |
| id       | int                                                        | ID       |
| prevdata | longtext *NULL*                                            | 旧值     |
| optype   | varchar(255) *NULL* [**CMDBChangeOpSetAttributeLongText**] | 操作类型 |

### 索引

| PRIMARY | *id*         |
| :------ | ------------ |
| INDEX   | *optype*(95) |