servicesubcategory

子服务 (ServiceSubcategory)



| 列           | 类型                                                     | 注释                                                         |
| :----------- | -------------------------------------------------------- | ------------------------------------------------------------ |
| id           | int *自动增量*                                           | 自增ID                                                       |
| name         | varchar(255) *NULL* []                                   | 名称                                                         |
| description  | text *NULL*                                              | 描述                                                         |
| service_id   | int *NULL* [**0**]                                       | 服务ID                                                       |
| request_type | enum('incident','service_request') *NULL* [**incident**] | 需求类型，事件 (incident), 服务需求 (service_request)        |
| status       | enum('implementation','obsolete','production') *NULL*    | 状态，启用 (implementation), 废弃 (obsolete), 生产 (production) |

### 索引

| PRIMARY | *id*         |
| :------ | ------------ |
| INDEX   | *name*(95)   |
| INDEX   | *service_id* |