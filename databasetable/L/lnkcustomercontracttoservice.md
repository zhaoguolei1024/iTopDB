lnkcustomercontracttoservice

关联 客户合同/服务 (lnkCustomerContractToService)



| 列                  | 类型               | 注释     |
| :------------------ | ------------------ | -------- |
| id                  | int *自动增量*     | 自增ID   |
| customercontract_id | int *NULL* [**0**] | 客户合同 |
| service_id          | int *NULL* [**0**] | 服务     |
| sla_id              | int *NULL* [**0**] | SLA      |

### 索引

| PRIMARY | *id*                  |
| :------ | --------------------- |
| INDEX   | *customercontract_id* |
| INDEX   | *service_id*          |
| INDEX   | *sla_id*              |