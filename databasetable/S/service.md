service



服务 (Service)



| 列               | 类型                                                  | 注释                                                         |
| :--------------- | ----------------------------------------------------- | ------------------------------------------------------------ |
| id               | int *自动增量*                                        | 自增ID                                                       |
| name             | varchar(255) *NULL* []                                | 名称                                                         |
| org_id           | int *NULL* [**0**]                                    | 组织                                                         |
| servicefamily_id | int *NULL* [**0**]                                    | 服务族                                                       |
| description      | text *NULL*                                           | 描述                                                         |
| status           | enum('implementation','obsolete','production') *NULL* | 状态，启用 (implementation), 废弃 (obsolete), 生产 (production) |
| icon_data        | longblob *NULL*                                       | 图标数据                                                     |
| icon_mimetype    | varchar(255) *NULL*                                   | 图标类型                                                     |
| icon_filename    | varchar(255) *NULL*                                   | 图标名称                                                     |

### 索引

| PRIMARY | *id*               |
| :------ | ------------------ |
| INDEX   | *name*(95)         |
| INDEX   | *org_id*           |
| INDEX   | *servicefamily_id* |