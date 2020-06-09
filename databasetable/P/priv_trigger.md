| 列          | 类型                              | 注释 |
| :---------- | --------------------------------- | ---- |
| id          | int *自动增量*                    |      |
| description | varchar(255) *NULL* []            |      |
| context     | varchar(255) *NULL* []            |      |
| realclass   | varchar(255) *NULL* [**Trigger**] |      |

### 索引

| PRIMARY | *id*              |
| :------ | ----------------- |
| INDEX   | *description*(95) |
| INDEX   | *realclass*(95)   |