priv_trigger_onstatechange

触发器 (当状态变化时) (TriggerOnStateChange) - 当对象状态变化时触发

触发器 (Trigger) >> 触发器 (class dependent) (TriggerOnObject) >> TriggerOnStateChange



| 列        | 类型                                           | 注释         |
| :-------- | ---------------------------------------------- | ------------ |
| id        | int *自动增量*                                 | 自增ID       |
| state     | varchar(255) *NULL* []                         | 状态         |
| realclass | varchar(255) *NULL* [**TriggerOnStateChange**] | 触发器子类别 |

### 索引

| PRIMARY | *id*            |
| :------ | --------------- |
| INDEX   | *realclass*(95) |