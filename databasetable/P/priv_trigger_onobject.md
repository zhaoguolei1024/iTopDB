

priv_trigger_onobject

触发器 (class dependent) (TriggerOnObject) - Trigger on a given class of objects

触发器 (Trigger) >> TriggerOnObject

| 列           | 类型                                                      | 注释         |
| :----------- | --------------------------------------------------------- | ------------ |
| id           | int *自动增量*                                            | 自增ID       |
| target_class | varchar(255) *NULL* [**TagSetFieldDataFor_FAQ__domains**] | 目标类       |
| filter       | text *NULL*                                               | 过滤器       |
| realclass    | varchar(255) *NULL* [**TriggerOnObject**]                 | 触发器子类别 |

### 索引

| PRIMARY | *id*               |
| :------ | ------------------ |
| INDEX   | *target_class*(95) |
| INDEX   | *realclass*(95)    |