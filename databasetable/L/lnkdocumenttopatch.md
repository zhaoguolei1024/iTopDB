| 列          | 类型               | 注释 |
| :---------- | ------------------ | ---- |
| id          | int *自动增量*     |      |
| patch_id    | int *NULL* [**0**] |      |
| document_id | int *NULL* [**0**] |      |

### 索引

| PRIMARY | *id*          |
| :------ | ------------- |
| INDEX   | *patch_id*    |
| INDEX   | *document_id* |