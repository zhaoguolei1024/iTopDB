lnkprovidercontracttoservice

关联 供应商合同/服务 (lnkProviderContractToService)



| 列                  | 类型               | 注释       |
| :------------------ | ------------------ | ---------- |
| id                  | int *自动增量*     | 自增ID     |
| service_id          | int *NULL* [**0**] | 服务       |
| providercontract_id | int *NULL* [**0**] | 供应商合同 |

### 索引

| PRIMARY | *id*                  |
| :------ | --------------------- |
| INDEX   | *service_id*          |
| INDEX   | *providercontract_id* |