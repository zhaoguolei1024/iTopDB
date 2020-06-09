| 列         | 类型                                        | 注释 |
| :--------- | ------------------------------------------- | ---- |
| id         | int *自动增量*                              |      |
| trigger_id | int *NULL* [**0**]                          |      |
| action_id  | int *NULL* [**0**]                          |      |
| object_id  | int *NULL* [**0**]                          |      |
| realclass  | varchar(255) *NULL* [**EventNotification**] |      |

### 索引

| PRIMARY | *id*            |
| :------ | --------------- |
| INDEX   | *trigger_id*    |
| INDEX   | *action_id*     |
| INDEX   | *realclass*(95) |
| INDEX   | *object_id*     |