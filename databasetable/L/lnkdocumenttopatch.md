lnkdocumenttopatch

链接 文档 / 补丁 (lnkDocumentToPatch)



| 列          | 类型               | 注释   |
| :---------- | ------------------ | ------ |
| id          | int *自动增量*     | 自增ID |
| patch_id    | int *NULL* [**0**] | 补丁   |
| document_id | int *NULL* [**0**] | 文档   |

### 索引

| PRIMARY | *id*          |
| :------ | ------------- |
| INDEX   | *patch_id*    |
| INDEX   | *document_id* |