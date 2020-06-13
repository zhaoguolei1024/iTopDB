priv_action_notification

通知 (ActionNotification) - 通知 (抽象)





| 列        | 类型                                         | 注释   |
| :-------- | -------------------------------------------- | ------ |
| id        | int *自动增量*                               | 自增ID |
| realclass | varchar(255) *NULL* [**ActionNotification**] |        |

### 索引

| PRIMARY | *id*            |
| :------ | --------------- |
| INDEX   | *realclass*(95) |