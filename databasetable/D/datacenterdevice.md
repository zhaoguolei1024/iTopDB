| 列           | 类型                                       | 注释 |
| :----------- | ------------------------------------------ | ---- |
| id           | int *自动增量*                             |      |
| rack_id      | int *NULL* [**0**]                         |      |
| enclosure_id | int *NULL* [**0**]                         |      |
| nb_u         | int *NULL*                                 |      |
| managementip | varchar(255) *NULL* []                     |      |
| powera_id    | int *NULL* [**0**]                         |      |
| powerB_id    | int *NULL* [**0**]                         |      |
| redundancy   | varchar(20) *NULL* [**1**]                 |      |
| finalclass   | varchar(255) *NULL* [**DatacenterDevice**] |      |

### 索引

| PRIMARY | *id*             |
| :------ | ---------------- |
| INDEX   | *rack_id*        |
| INDEX   | *enclosure_id*   |
| INDEX   | *powera_id*      |
| INDEX   | *powerB_id*      |
| INDEX   | *finalclass*(95) |