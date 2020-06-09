| 列          | 类型               | 注释 |
| :---------- | ------------------ | ---- |
| id          | int *自动增量*     |      |
| software_id | int *NULL* [**0**] |      |
| document_id | int *NULL* [**0**] |      |

### 索引

| PRIMARY | *id*          |
| :------ | ------------- |
| INDEX   | *software_id* |
| INDEX   | *document_id* |