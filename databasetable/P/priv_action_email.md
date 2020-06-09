| 列             | 类型                                            | 注释 |
| :------------- | ----------------------------------------------- | ---- |
| id             | int *自动增量*                                  |      |
| test_recipient | varchar(255) *NULL* []                          |      |
| from           | varchar(255) *NULL* []                          |      |
| reply_to       | varchar(255) *NULL* []                          |      |
| to             | text *NULL*                                     |      |
| cc             | text *NULL*                                     |      |
| bcc            | text *NULL*                                     |      |
| subject        | varchar(255) *NULL* []                          |      |
| body           | text *NULL*                                     |      |
| importance     | enum('high','low','normal') *NULL* [**normal**] |      |

### 索引

| PRIMARY | *id* |
| :------ | ---- |
|         |      |