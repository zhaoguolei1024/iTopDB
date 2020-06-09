| 列          | 类型                                                         | 注释 |
| :---------- | ------------------------------------------------------------ | ---- |
| id          | int *自动增量*                                               |      |
| ticket_id   | int *NULL* [**0**]                                           |      |
| contact_id  | int *NULL* [**0**]                                           |      |
| role        | varchar(255) *NULL* []                                       |      |
| impact_code | enum('computed','do_not_notify','manual') *NULL* [**manual**] |      |

### 索引

| PRIMARY | *id*         |
| :------ | ------------ |
| INDEX   | *ticket_id*  |
| INDEX   | *contact_id* |