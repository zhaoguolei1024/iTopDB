| 列                 | 类型                                                     | 注释 |
| :----------------- | -------------------------------------------------------- | ---- |
| id                 | int *自动增量*                                           |      |
| operational_status | enum('closed','ongoing','resolved') *NULL* [**ongoing**] |      |
| ref                | varchar(255) *NULL* []                                   |      |
| org_id             | int *NULL* [**0**]                                       |      |
| caller_id          | int *NULL* [**0**]                                       |      |
| team_id            | int *NULL* [**0**]                                       |      |
| agent_id           | int *NULL* [**0**]                                       |      |
| title              | varchar(255) *NULL* []                                   |      |
| description        | text *NULL*                                              |      |
| description_format | enum('text','html') *NULL* [**text**]                    |      |
| start_date         | datetime *NULL*                                          |      |
| end_date           | datetime *NULL*                                          |      |
| last_update        | datetime *NULL*                                          |      |
| close_date         | datetime *NULL*                                          |      |
| private_log        | longtext *NULL*                                          |      |
| private_log_index  | blob *NULL*                                              |      |
| finalclass         | varchar(255) *NULL* [**Ticket**]                         |      |

### 索引

| PRIMARY | *id*                 |
| :------ | -------------------- |
| INDEX   | *operational_status* |
| INDEX   | *ref*(95)            |
| INDEX   | *org_id*             |
| INDEX   | *caller_id*          |
| INDEX   | *team_id*            |
| INDEX   | *agent_id*           |
| INDEX   | *finalclass*(95)     |