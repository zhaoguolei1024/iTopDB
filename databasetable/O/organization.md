| 列                | 类型                                          | 注释 |
| :---------------- | --------------------------------------------- | ---- |
| id                | int *自动增量*                                |      |
| name              | varchar(255) *NULL* []                        |      |
| code              | varchar(255) *NULL* []                        |      |
| status            | enum('active','inactive') *NULL* [**active**] |      |
| parent_id         | int *NULL* [**0**]                            |      |
| parent_id_left    | int *NULL* [**0**]                            |      |
| parent_id_right   | int *NULL* [**0**]                            |      |
| deliverymodel_id  | int *NULL* [**0**]                            |      |
| obsolescence_date | date *NULL*                                   |      |

### 索引

| PRIMARY | *id*               |
| :------ | ------------------ |
| INDEX   | *name*(95)         |
| INDEX   | *parent_id*        |
| INDEX   | *parent_id_left*   |
| INDEX   | *parent_id_right*  |
| INDEX   | *deliverymodel_id* |