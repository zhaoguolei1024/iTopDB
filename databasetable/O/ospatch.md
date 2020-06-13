ospatch

操作系统补丁 (OSPatch)





| 列           | 类型               | 注释         |
| :----------- | ------------------ | ------------ |
| id           | int *自动增量*     | 自增ID       |
| osversion_id | int *NULL* [**0**] | 操作系统版本 |

### 索引

| PRIMARY | *id*           |
| :------ | -------------- |
| INDEX   | *osversion_id* |