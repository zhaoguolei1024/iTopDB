| 列               | 类型               | 注释 |
| :--------------- | ------------------ | ---- |
| id               | int *自动增量*     |      |
| deliverymodel_id | int *NULL* [**0**] |      |
| contact_id       | int *NULL* [**0**] |      |
| role_id          | int *NULL* [**0**] |      |

### 索引

| PRIMARY | *id*               |
| :------ | ------------------ |
| INDEX   | *deliverymodel_id* |
| INDEX   | *contact_id*       |
| INDEX   | *role_id*          |