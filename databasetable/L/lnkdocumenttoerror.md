lnkdocumenttoerror



关联 文档/已知问题 (lnkDocumentToError) - 文档和已知问题之间的关联



| 列          | 类型                   | 注释     |
| :---------- | ---------------------- | -------- |
| link_id     | int *自动增量*         | 自增ID   |
| document_id | int *NULL* [**0**]     | 文档     |
| error_id    | int *NULL* [**0**]     | 已知问题 |
| link_type   | varchar(255) *NULL* [] | 关联类型 |

### 索引

| PRIMARY | *link_id*       |
| :------ | --------------- |
| INDEX   | *document_id*   |
| INDEX   | *error_id*      |
| INDEX   | *link_type*(95) |