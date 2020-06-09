| 列                         | 类型                                                         | 注释 |
| :------------------------- | ------------------------------------------------------------ | ---- |
| id                         | int *自动增量*                                               |      |
| status                     | enum('assigned','closed','escalated_tto','escalated_ttr','new','pending','resolved') *NULL* [**new**] |      |
| impact                     | enum('1','2','3') *NULL* [**1**]                             |      |
| priority                   | enum('1','2','3','4') *NULL* [**4**]                         |      |
| urgency                    | enum('1','2','3','4') *NULL* [**4**]                         |      |
| origin                     | enum('mail','monitoring','phone','portal') *NULL* [**phone**] |      |
| service_id                 | int *NULL* [**0**]                                           |      |
| servicesubcategory_id      | int *NULL* [**0**]                                           |      |
| escalation_flag            | enum('no','yes') *NULL* [**no**]                             |      |
| escalation_reason          | varchar(255) *NULL* []                                       |      |
| assignment_date            | datetime *NULL*                                              |      |
| resolution_date            | datetime *NULL*                                              |      |
| last_pending_date          | datetime *NULL*                                              |      |
| cumulatedpending_timespent | int unsigned *NULL*                                          |      |
| cumulatedpending_started   | datetime *NULL*                                              |      |
| cumulatedpending_laststart | datetime *NULL*                                              |      |
| cumulatedpending_stopped   | datetime *NULL*                                              |      |
| tto_timespent              | int unsigned *NULL*                                          |      |
| tto_started                | datetime *NULL*                                              |      |
| tto_laststart              | datetime *NULL*                                              |      |
| tto_stopped                | datetime *NULL*                                              |      |
| tto_75_deadline            | datetime *NULL*                                              |      |
| tto_75_passed              | tinyint unsigned *NULL*                                      |      |
| tto_75_triggered           | tinyint(1) *NULL*                                            |      |
| tto_75_overrun             | int unsigned *NULL*                                          |      |
| tto_100_deadline           | datetime *NULL*                                              |      |
| tto_100_passed             | tinyint unsigned *NULL*                                      |      |
| tto_100_triggered          | tinyint(1) *NULL*                                            |      |
| tto_100_overrun            | int unsigned *NULL*                                          |      |
| ttr_timespent              | int unsigned *NULL*                                          |      |
| ttr_started                | datetime *NULL*                                              |      |
| ttr_laststart              | datetime *NULL*                                              |      |
| ttr_stopped                | datetime *NULL*                                              |      |
| ttr_75_deadline            | datetime *NULL*                                              |      |
| ttr_75_passed              | tinyint unsigned *NULL*                                      |      |
| ttr_75_triggered           | tinyint(1) *NULL*                                            |      |
| ttr_75_overrun             | int unsigned *NULL*                                          |      |
| ttr_100_deadline           | datetime *NULL*                                              |      |
| ttr_100_passed             | tinyint unsigned *NULL*                                      |      |
| ttr_100_triggered          | tinyint(1) *NULL*                                            |      |
| ttr_100_overrun            | int unsigned *NULL*                                          |      |
| time_spent                 | int unsigned *NULL*                                          |      |
| resolution_code            | enum('assistance','bug fixed','hardware repair','other','software patch','system update','training') *NULL* [**assistance**] |      |
| solution                   | text *NULL*                                                  |      |
| pending_reason             | text *NULL*                                                  |      |
| parent_incident_id         | int *NULL* [**0**]                                           |      |
| parent_problem_id          | int *NULL* [**0**]                                           |      |
| parent_change_id           | int *NULL* [**0**]                                           |      |
| public_log                 | longtext *NULL*                                              |      |
| public_log_index           | blob *NULL*                                                  |      |
| user_satisfaction          | enum('1','2','3','4') *NULL* [**1**]                         |      |
| user_commment              | text *NULL*                                                  |      |

### 索引

| PRIMARY | *id*                    |
| :------ | ----------------------- |
| INDEX   | *service_id*            |
| INDEX   | *servicesubcategory_id* |
| INDEX   | *parent_incident_id*    |
| INDEX   | *parent_problem_id*     |
| INDEX   | *parent_change_id*      |