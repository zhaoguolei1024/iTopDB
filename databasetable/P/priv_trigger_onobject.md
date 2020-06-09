| 列           | 类型                                                      | 注释 |
| :----------- | --------------------------------------------------------- | ---- |
| id           | int *自动增量*                                            |      |
| target_class | varchar(255) *NULL* [**TagSetFieldDataFor_FAQ__domains**] |      |
| filter       | text *NULL*                                               |      |
| realclass    | varchar(255) *NULL* [**TriggerOnObject**]                 |      |

### 索引

| PRIMARY | *id*               |
| :------ | ------------------ |
| INDEX   | *target_class*(95) |
| INDEX   | *realclass*(95)    |