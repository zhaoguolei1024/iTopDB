| 列                    | 类型                                                        | 注释 |
| :-------------------- | ----------------------------------------------------------- | ---- |
| id                    | int *自动增量*                                              |      |
| status                | enum('assigned','closed','new','resolved') *NULL* [**new**] |      |
| service_id            | int *NULL* [**0**]                                          |      |
| servicesubcategory_id | int *NULL* [**0**]                                          |      |
| product               | varchar(255) *NULL* []                                      |      |
| impact                | enum('1','2','3') *NULL* [**1**]                            |      |
| urgency               | enum('1','2','3','4') *NULL* [**1**]                        |      |
| priority              | enum('1','2','3','4') *NULL* [**1**]                        |      |
| related_change_id     | int *NULL* [**0**]                                          |      |
| assignment_date       | datetime *NULL*                                             |      |
| resolution_date       | datetime *NULL*                                             |      |

### 索引

| PRIMARY | *id*                    |
| :------ | ----------------------- |
| INDEX   | *service_id*            |
| INDEX   | *servicesubcategory_id* |
| INDEX   | *related_change_id*     |