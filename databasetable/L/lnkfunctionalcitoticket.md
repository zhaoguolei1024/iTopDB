| 列              | 类型                                                         | 注释 |
| :-------------- | ------------------------------------------------------------ | ---- |
| id              | int *自动增量*                                               |      |
| ticket_id       | int *NULL* [**0**]                                           |      |
| functionalci_id | int *NULL* [**0**]                                           |      |
| impact          | varchar(255) *NULL* []                                       |      |
| impact_code     | enum('computed','manual','not_impacted') *NULL* [**manual**] |      |

### 索引

| PRIMARY | *id*              |
| :------ | ----------------- |
| INDEX   | *ticket_id*       |
| INDEX   | *functionalci_id* |