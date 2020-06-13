priv_event



日志事件 (Event) - 应用程序的内部事件



| 列        | 类型                            | 注释       |
| :-------- | ------------------------------- | ---------- |
| id        | int *自动增量*                  | ID         |
| message   | text *NULL*                     | 消息       |
| date      | datetime *NULL*                 | 日期       |
| userinfo  | varchar(255) *NULL* []          | 用户信息   |
| realclass | varchar(255) *NULL* [**Event**] | 事件子类别 |

### 索引

| PRIMARY | *id*            |
| :------ | --------------- |
| INDEX   | *realclass*(95) |