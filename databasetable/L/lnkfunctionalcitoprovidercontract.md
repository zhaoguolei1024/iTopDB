lnkfunctionalcitoprovidercontract

关联 功能配置项/供应商合同 (lnkFunctionalCIToProviderContract)



| 列                  | 类型               | 注释       |
| :------------------ | ------------------ | ---------- |
| id                  | int *自动增量*     | 自增ID     |
| providercontract_id | int *NULL* [**0**] | 供应商合同 |
| functionalci_id     | int *NULL* [**0**] | 配置项     |

### 索引

| PRIMARY | *id*                  |
| :------ | --------------------- |
| INDEX   | *providercontract_id* |
| INDEX   | *functionalci_id*     |