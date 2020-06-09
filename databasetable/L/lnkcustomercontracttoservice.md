| 列                  | 类型               | 注释 |
| :------------------ | ------------------ | ---- |
| id                  | int *自动增量*     |      |
| customercontract_id | int *NULL* [**0**] |      |
| service_id          | int *NULL* [**0**] |      |
| sla_id              | int *NULL* [**0**] |      |

### 索引

| PRIMARY | *id*                  |
| :------ | --------------------- |
| INDEX   | *customercontract_id* |
| INDEX   | *service_id*          |
| INDEX   | *sla_id*              |