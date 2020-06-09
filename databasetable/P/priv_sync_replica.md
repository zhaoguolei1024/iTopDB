| 列                  | 类型                                                         | 注释 |
| :------------------ | ------------------------------------------------------------ | ---- |
| id                  | int *自动增量*                                               |      |
| sync_source_id      | int *NULL* [**0**]                                           |      |
| dest_id             | int *NULL* [**0**]                                           |      |
| dest_class          | varchar(255) *NULL* [**Organization**]                       |      |
| status_last_seen    | datetime *NULL*                                              |      |
| status              | enum('modified','new','obsolete','orphan','synchronized') *NULL* [**new**] |      |
| status_dest_creator | tinyint(1) *NULL* [**0**]                                    |      |
| status_last_error   | varchar(255) *NULL* []                                       |      |
| status_last_warning | varchar(255) *NULL* []                                       |      |
| info_creation_date  | datetime *NULL*                                              |      |
| info_last_modified  | datetime *NULL*                                              |      |

### 索引

| PRIMARY | *id*                        |
| :------ | --------------------------- |
| INDEX   | *sync_source_id*            |
| INDEX   | *dest_class*(95)            |
| INDEX   | *dest_class*(95), *dest_id* |