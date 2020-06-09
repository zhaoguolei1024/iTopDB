| 列     | 类型               | 注释 |
| :----- | ------------------ | ---- |
| id     | int *自动增量*     |      |
| sla_id | int *NULL* [**0**] |      |
| slt_id | int *NULL* [**0**] |      |

### 索引

| PRIMARY | *id*     |
| :------ | -------- |
| INDEX   | *sla_id* |
| INDEX   | *slt_id* |