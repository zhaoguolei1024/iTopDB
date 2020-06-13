lnkcontacttofunctionalci



链接 联系人 / 功能项 (lnkContactToFunctionalCI)



| 列              | 类型               | 注释   |
| :-------------- | ------------------ | ------ |
| id              | int *自动增量*     | 自增ID |
| functionalci_id | int *NULL* [**0**] | 功能项 |
| contact_id      | int *NULL* [**0**] | 联系人 |

### 索引

| PRIMARY | *id*              |
| :------ | ----------------- |
| INDEX   | *functionalci_id* |
| INDEX   | *contact_id*      |