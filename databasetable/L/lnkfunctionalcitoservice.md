lnkfunctionalcitoservice

关联 功能配置项/服务 (lnkFunctionalCIToService)



| 列              | 类型               | 注释   |
| :-------------- | ------------------ | ------ |
| id              | int *自动增量*     | 自增ID |
| service_id      | int *NULL* [**0**] | 服务   |
| functionalci_id | int *NULL* [**0**] | 配置项 |

### 索引

| PRIMARY | *id*              |
| :------ | ----------------- |
| INDEX   | *service_id*      |
| INDEX   | *functionalci_id* |