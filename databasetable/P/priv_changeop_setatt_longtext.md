| 列       | 类型                                                       | 注释 |
| :------- | ---------------------------------------------------------- | ---- |
| id       | int                                                        |      |
| prevdata | longtext *NULL*                                            |      |
| optype   | varchar(255) *NULL* [**CMDBChangeOpSetAttributeLongText**] |      |

### 索引

| PRIMARY | *id*         |
| :------ | ------------ |
| INDEX   | *optype*(95) |