priv_event_loginusage

登录频率 (EventLoginUsage) - Connection to the application

日志事件 (Event) >> EventLoginUsage



| 列      | 类型               | 注释     |
| :------ | ------------------ | -------- |
| id      | int *自动增量*     | 自增ID   |
| user_id | int *NULL* [**0**] | 登录用户 |

### 索引

| PRIMARY | *id*      |
| :------ | --------- |
| INDEX   | *user_id* |