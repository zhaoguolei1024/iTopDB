lnkcontracttodocument

关联 合同/文档 (lnkContractToDocument)





| 列          | 类型               | 注释   |
| :---------- | ------------------ | ------ |
| id          | int *自动增量*     | 自增ID |
| contract_id | int *NULL* [**0**] | 合同   |
| document_id | int *NULL* [**0**] | 文档   |

### 索引

| PRIMARY | *id*          |
| :------ | ------------- |
| INDEX   | *contract_id* |
| INDEX   | *document_id* |