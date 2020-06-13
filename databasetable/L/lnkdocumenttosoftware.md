lnkdocumenttosoftware



链接 文档 / 软件 (lnkDocumentToSoftware)



| 列          | 类型               | 注释   |
| :---------- | ------------------ | ------ |
| id          | int *自动增量*     | 自增ID |
| software_id | int *NULL* [**0**] | 软件   |
| document_id | int *NULL* [**0**] | 文档   |

### 索引

| PRIMARY | *id*          |
| :------ | ------------- |
| INDEX   | *software_id* |
| INDEX   | *document_id* |