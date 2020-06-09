| 列                  | 类型                                                         | 注释 |
| :------------------ | ------------------------------------------------------------ | ---- |
| id                  | int *自动增量*                                               |      |
| status              | enum('approved','assigned','closed','implemented','monitored','new','notapproved','plannedscheduled','rejected','validated') *NULL* [**new**] |      |
| reason              | varchar(255) *NULL* []                                       |      |
| requestor_id        | int *NULL* [**0**]                                           |      |
| creation_date       | datetime *NULL*                                              |      |
| impact              | varchar(255) *NULL* []                                       |      |
| supervisor_group_id | int *NULL* [**0**]                                           |      |
| supervisor_id       | int *NULL* [**0**]                                           |      |
| manager_group_id    | int *NULL* [**0**]                                           |      |
| manager_id          | int *NULL* [**0**]                                           |      |
| outage              | enum('no','yes') *NULL* [**no**]                             |      |
| fallback            | text *NULL*                                                  |      |
| parent_id           | int *NULL* [**0**]                                           |      |
| finalclass          | varchar(255) *NULL* [**Change**]                             |      |

### 索引

| PRIMARY | *id*                  |
| :------ | --------------------- |
| INDEX   | *requestor_id*        |
| INDEX   | *supervisor_group_id* |
| INDEX   | *supervisor_id*       |
| INDEX   | *manager_group_id*    |
| INDEX   | *manager_id*          |
| INDEX   | *parent_id*           |
| INDEX   | *finalclass*(95)      |