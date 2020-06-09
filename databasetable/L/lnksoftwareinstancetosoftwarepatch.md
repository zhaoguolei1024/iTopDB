| 列                  | 类型               | 注释 |
| :------------------ | ------------------ | ---- |
| id                  | int *自动增量*     |      |
| softwarepatch_id    | int *NULL* [**0**] |      |
| softwareinstance_id | int *NULL* [**0**] |      |

### 索引

| PRIMARY | *id*                  |
| :------ | --------------------- |
| INDEX   | *softwarepatch_id*    |
| INDEX   | *softwareinstance_id* |