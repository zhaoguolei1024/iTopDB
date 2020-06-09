| 列          | 类型                                                | 注释 |
| :---------- | --------------------------------------------------- | ---- |
| id          | int *自动增量*                                      |      |
| name        | varchar(255) *NULL* []                              |      |
| description | varchar(255) *NULL* []                              |      |
| status      | enum('test','enabled','disabled') *NULL* [**test**] |      |
| realclass   | varchar(255) *NULL* [**Action**]                    |      |

### 索引

| PRIMARY | *id*            |
| :------ | --------------- |
| INDEX   | *name*(95)      |
| INDEX   | *realclass*(95) |