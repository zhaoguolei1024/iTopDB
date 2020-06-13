lnkcontacttocontract

关联 联系人/合同 (lnkContactToContract)



| 列          | 类型               | 注释   |
| :---------- | ------------------ | ------ |
| id          | int *自动增量*     | 自增ID |
| contract_id | int *NULL* [**0**] | 合同   |
| contact_id  | int *NULL* [**0**] | 联系人 |

### 索引

| PRIMARY | *id*          |
| :------ | ------------- |
| INDEX   | *contract_id* |
| INDEX   | *contact_id*  |