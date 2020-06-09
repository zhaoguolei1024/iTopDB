| 列         | 类型               | 注释 |
| :--------- | ------------------ | ---- |
| link_id    | int *自动增量*     |      |
| action_id  | int *NULL* [**0**] |      |
| trigger_id | int *NULL* [**0**] |      |
| order      | int *NULL* [**0**] |      |

### 索引

| PRIMARY | *link_id*    |
| :------ | ------------ |
| INDEX   | *action_id*  |
| INDEX   | *trigger_id* |