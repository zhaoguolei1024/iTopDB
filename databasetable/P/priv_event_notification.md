priv_event_notification

通知事件 (EventNotification) - Trace of a notification that has been sent

日志事件 (Event) >> EventNotification



| 列         | 类型                                        | 注释       |
| :--------- | ------------------------------------------- | ---------- |
| id         | int *自动增量*                              | 自增ID     |
| trigger_id | int *NULL* [**0**]                          | 触发器     |
| action_id  | int *NULL* [**0**]                          | 用户       |
| object_id  | int *NULL* [**0**]                          | 对象id     |
| realclass  | varchar(255) *NULL* [**EventNotification**] | 事件子类别 |

### 索引

| PRIMARY | *id*            |
| :------ | --------------- |
| INDEX   | *trigger_id*    |
| INDEX   | *action_id*     |
| INDEX   | *realclass*(95) |
| INDEX   | *object_id*     |