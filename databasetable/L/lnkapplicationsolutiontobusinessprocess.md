| 列                     | 类型               | 注释 |
| :--------------------- | ------------------ | ---- |
| id                     | int *自动增量*     |      |
| businessprocess_id     | int *NULL* [**0**] |      |
| applicationsolution_id | int *NULL* [**0**] |      |

### 索引

| PRIMARY | *id*                     |
| :------ | ------------------------ |
| INDEX   | *businessprocess_id*     |
| INDEX   | *applicationsolution_id* |