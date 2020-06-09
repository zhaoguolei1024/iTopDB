| 列                   | 类型               | 注释 |
| :------------------- | ------------------ | ---- |
| id                   | int *自动增量*     |      |
| physicalinterface_id | int *NULL* [**0**] |      |
| vlan_id              | int *NULL* [**0**] |      |

### 索引

| PRIMARY | *id*                   |
| :------ | ---------------------- |
| INDEX   | *physicalinterface_id* |
| INDEX   | *vlan_id*              |