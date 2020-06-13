priv_trigger_threshold

触发器 (基于阀值) (TriggerOnThresholdReached) - 当达到某个阀值时触发

触发器 (Trigger) >> 触发器 (class dependent) (TriggerOnObject) >> TriggerOnThresholdReached



| 列              | 类型                   | 注释   |
| :-------------- | ---------------------- | ------ |
| id              | int *自动增量*         | 自增ID |
| stop_watch_code | varchar(255) *NULL* [] | 秒表   |
| threshold_index | varchar(255) *NULL* [] | 阀值   |

### 索引

| PRIMARY | *id* |
| :------ | ---- |
|         |      |