| 列        | 类型               | 注释 |
| :-------- | ------------------ | ---- |
| id        | int *自动增量*     |      |
| subnet_id | int *NULL* [**0**] |      |
| vlan_id   | int *NULL* [**0**] |      |

### 索引

| PRIMARY | *id*        |
| :------ | ----------- |
| INDEX   | *subnet_id* |
| INDEX   | *vlan_id*   |