

priv_async_send_email

Email (异步) (AsyncSendEmail)

异步任务 (AsyncTask) >> AsyncSendEmail



| 列      | 类型               | 注释     |
| :------ | ------------------ | -------- |
| id      | int *自动增量*     | 自增ID   |
| version | int *NULL* [**1**] | 版本号   |
| to      | text *NULL*        | 收件人   |
| subject | text *NULL*        | 主题     |
| message | longtext *NULL*    | 消息内容 |

### 索引

| PRIMARY | *id* |
| :------ | ---- |
|         |      |