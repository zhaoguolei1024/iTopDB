| 列          | 类型               | 注释 |
| :---------- | ------------------ | ---- |
| id          | int *自动增量*     |      |
| licence_id  | int *NULL* [**0**] |      |
| document_id | int *NULL* [**0**] |      |

### 索引

| PRIMARY | *id*          |
| :------ | ------------- |
| INDEX   | *licence_id*  |
| INDEX   | *document_id* |