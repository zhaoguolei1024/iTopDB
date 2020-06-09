| 列                | 类型                                                         | 注释 |
| :---------------- | ------------------------------------------------------------ | ---- |
| id                | int *自动增量*                                               |      |
| name              | varchar(255) *NULL* []                                       |      |
| status            | enum('implementation','obsolete','production') *NULL* [**implementation**] |      |
| org_id            | int *NULL* [**0**]                                           |      |
| description       | text *NULL*                                                  |      |
| type              | varchar(255) *NULL* []                                       |      |
| parent_id         | int *NULL* [**0**]                                           |      |
| parent_id_left    | int *NULL* [**0**]                                           |      |
| parent_id_right   | int *NULL* [**0**]                                           |      |
| obsolescence_date | date *NULL*                                                  |      |

### 索引

| PRIMARY | *id*              |
| :------ | ----------------- |
| INDEX   | *name*(95)        |
| INDEX   | *org_id*          |
| INDEX   | *parent_id*       |
| INDEX   | *parent_id_left*  |
| INDEX   | *parent_id_right* |