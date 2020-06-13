organization

组织 (Organization)



| 列                | 类型                                          | 注释                                 |
| :---------------- | --------------------------------------------- | ------------------------------------ |
| id                | int *自动增量*                                | 自增ID                               |
| name              | varchar(255) *NULL* []                        | 名称                                 |
| code              | varchar(255) *NULL* []                        | 编码                                 |
| status            | enum('active','inactive') *NULL* [**active**] | 状态，启用 (active), 停用 (inactive) |
| parent_id         | int *NULL* [**0**]                            | 父级                                 |
| parent_id_left    | int *NULL* [**0**]                            |                                      |
| parent_id_right   | int *NULL* [**0**]                            |                                      |
| deliverymodel_id  | int *NULL* [**0**]                            | 交付模式                             |
| obsolescence_date | date *NULL*                                   | 废弃时间                             |

### 索引

| PRIMARY | *id*               |
| :------ | ------------------ |
| INDEX   | *name*(95)         |
| INDEX   | *parent_id*        |
| INDEX   | *parent_id_left*   |
| INDEX   | *parent_id_right*  |
| INDEX   | *deliverymodel_id* |