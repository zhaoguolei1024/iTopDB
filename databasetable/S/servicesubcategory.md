| 列           | 类型                                                     | 注释 |
| :----------- | -------------------------------------------------------- | ---- |
| id           | int *自动增量*                                           |      |
| name         | varchar(255) *NULL* []                                   |      |
| description  | text *NULL*                                              |      |
| service_id   | int *NULL* [**0**]                                       |      |
| request_type | enum('incident','service_request') *NULL* [**incident**] |      |
| status       | enum('implementation','obsolete','production') *NULL*    |      |

### 索引

| PRIMARY | *id*         |
| :------ | ------------ |
| INDEX   | *name*(95)   |
| INDEX   | *service_id* |