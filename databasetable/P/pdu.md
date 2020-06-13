pdu

PDU (PDU)

功能配置项 (FunctionalCI) >> 物理设备 (PhysicalDevice) >> 电源连接 (PowerConnection) >> PDU

| 列            | 类型               | 注释     |
| :------------ | ------------------ | -------- |
| id            | int *自动增量*     | 自增ID   |
| rack_id       | int *NULL* [**0**] | 机柜     |
| powerstart_id | int *NULL* [**0**] | 上级电源 |

### 索引

| PRIMARY | *id*            |
| :------ | --------------- |
| INDEX   | *rack_id*       |
| INDEX   | *powerstart_id* |