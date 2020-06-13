group

配置组 (Group)



| 列                | 类型                                                         | 注释                                                         |
| :---------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| id                | int *自动增量*                                               | 自增ID                                                       |
| name              | varchar(255) *NULL* []                                       | 名称                                                         |
| status            | enum('implementation','obsolete','production') *NULL* [**implementation**] | 状态，上线 (implementation), 废弃 (obsolete), 生产 (production) |
| org_id            | int *NULL* [**0**]                                           | 组织                                                         |
| description       | text *NULL*                                                  | 描述                                                         |
| type              | varchar(255) *NULL* []                                       | 类型                                                         |
| parent_id         | int *NULL* [**0**]                                           | 上级组                                                       |
| parent_id_left    | int *NULL* [**0**]                                           |                                                              |
| parent_id_right   | int *NULL* [**0**]                                           |                                                              |
| obsolescence_date | date *NULL*                                                  | 废弃时间                                                     |

### 索引

| PRIMARY | *id*              |
| :------ | ----------------- |
| INDEX   | *name*(95)        |
| INDEX   | *org_id*          |
| INDEX   | *parent_id*       |
| INDEX   | *parent_id_left*  |
| INDEX   | *parent_id_right* |