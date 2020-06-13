lnkdocumenttolicence

链接 文档 / 许可证 (lnkDocumentToLicence)



| 列          | 类型               | 注释   |
| :---------- | ------------------ | ------ |
| id          | int *自动增量*     | 自增ID |
| licence_id  | int *NULL* [**0**] | 许可证 |
| document_id | int *NULL* [**0**] | 文档   |

### 索引

| PRIMARY | *id*          |
| :------ | ------------- |
| INDEX   | *licence_id*  |
| INDEX   | *document_id* |