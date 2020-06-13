physicalinterface

物理网卡 (PhysicalInterface)

网卡 (NetworkInterface) >> IP Interface (IPInterface) >> PhysicalInterface



| 列               | 类型               | 注释   |
| :--------------- | ------------------ | ------ |
| id               | int *自动增量*     | 自增ID |
| connectableci_id | int *NULL* [**0**] | 设备   |

### 索引

| PRIMARY | *id*               |
| :------ | ------------------ |
| INDEX   | *connectableci_id* |