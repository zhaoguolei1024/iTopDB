lnkdocumenttofunctionalci



链接 文档 / 功能项 (lnkDocumentToFunctionalCI)



| 列              | 类型               | 注释   |
| :-------------- | ------------------ | ------ |
| id              | int *自动增量*     | 自增ID |
| functionalci_id | int *NULL* [**0**] | 功能项 |
| document_id     | int *NULL* [**0**] | 文档   |

### 索引

| PRIMARY | *id*              |
| :------ | ----------------- |
| INDEX   | *functionalci_id* |
| INDEX   | *document_id*     |