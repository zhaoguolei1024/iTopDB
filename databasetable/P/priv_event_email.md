priv_event_email

邮件发送事件 (EventNotificationEmail) - 跟踪每封已发送的邮件

日志事件 (Event) >> 通知事件 (EventNotification) >> EventNotificationEmail



| 列          | 类型            | 注释   |
| :---------- | --------------- | ------ |
| id          | int *自动增量*  | ID     |
| to          | text *NULL*     | 收件人 |
| cc          | text *NULL*     | 抄送   |
| bcc         | text *NULL*     | 密抄   |
| from        | text *NULL*     | 发件人 |
| subject     | text *NULL*     | 主题   |
| body        | longtext *NULL* | 内容   |
| attachments | longtext *NULL* | 附件   |

### 索引

| PRIMARY | *id* |
| :------ | ---- |
|         |      |