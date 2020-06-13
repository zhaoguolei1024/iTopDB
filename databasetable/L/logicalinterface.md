logicalinterface

逻辑网卡 (LogicalInterface)

网卡 (NetworkInterface) >> IP Interface (IPInterface) >> LogicalInterface



| 列                | 类型               | 注释   |
| :---------------- | ------------------ | ------ |
| id                | int *自动增量*     | 自增ID |
| virtualmachine_id | int *NULL* [**0**] | 虚拟机 |

### 索引

| PRIMARY | *id*                |
| :------ | ------------------- |
| INDEX   | *virtualmachine_id* |