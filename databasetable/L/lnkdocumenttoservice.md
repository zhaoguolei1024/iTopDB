lnkdocumenttoservice

关联 文档/服务 (lnkDocumentToService)



| 列          | 类型               | 注释   |
| :---------- | ------------------ | ------ |
| id          | int *自动增量*     | 自增ID |
| service_id  | int *NULL* [**0**] | 服务   |
| document_id | int *NULL* [**0**] | 文档   |

### 索引

| PRIMARY | *id*          |
| :------ | ------------- |
| INDEX   | *service_id*  |
| INDEX   | *document_id* |