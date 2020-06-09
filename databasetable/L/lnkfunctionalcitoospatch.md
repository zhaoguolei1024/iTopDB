| 列              | 类型               | 注释 |
| :-------------- | ------------------ | ---- |
| id              | int *自动增量*     |      |
| ospatch_id      | int *NULL* [**0**] |      |
| functionalci_id | int *NULL* [**0**] |      |

### 索引

| PRIMARY | *id*              |
| :------ | ----------------- |
| INDEX   | *ospatch_id*      |
| INDEX   | *functionalci_id* |