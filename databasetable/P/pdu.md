| 列            | 类型               | 注释 |
| :------------ | ------------------ | ---- |
| id            | int *自动增量*     |      |
| rack_id       | int *NULL* [**0**] |      |
| powerstart_id | int *NULL* [**0**] |      |

### 索引

| PRIMARY | *id*            |
| :------ | --------------- |
| INDEX   | *rack_id*       |
| INDEX   | *powerstart_id* |