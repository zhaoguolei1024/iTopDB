priv_action_email

邮件通知 (ActionEmail)

自定义操作 (Action) >> 通知 (ActionNotification) >> ActionEmail



| 列             | 类型                                            | 注释                                       |
| :------------- | ----------------------------------------------- | ------------------------------------------ |
| id             | int *自动增量*                                  | 自增ID                                     |
| test_recipient | varchar(255) *NULL* []                          | 测试收件人                                 |
| from           | varchar(255) *NULL* []                          | 发件人                                     |
| reply_to       | varchar(255) *NULL* []                          | 回复到                                     |
| to             | text *NULL*                                     | 收件人                                     |
| cc             | text *NULL*                                     | 抄送                                       |
| bcc            | text *NULL*                                     | 密抄                                       |
| subject        | varchar(255) *NULL* []                          | 主题                                       |
| body           | text *NULL*                                     | 正文                                       |
| importance     | enum('high','low','normal') *NULL* [**normal**] | 重要性，高 (high), 低 (low), 普通 (normal) |

### 索引

| PRIMARY | *id* |
| :------ | ---- |
|         |      |