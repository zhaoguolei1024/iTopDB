| 列         | 类型               | 注释 |
| :--------- | ------------------ | ---- |
| id         | int *自动增量*     |      |
| service_id | int *NULL* [**0**] |      |
| contact_id | int *NULL* [**0**] |      |

### 索引

| PRIMARY | *id*         |
| :------ | ------------ |
| INDEX   | *service_id* |
| INDEX   | *contact_id* |