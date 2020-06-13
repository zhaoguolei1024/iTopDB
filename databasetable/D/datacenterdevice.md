datacenterdevice

数据中心设备

功能配置项 (FunctionalCI) >> 物理设备 (PhysicalDevice) >> 可连接的配置项 (ConnectableCI) >> DatacenterDevice

| 列           | 类型                                       | 注释            |
| :----------- | ------------------------------------------ | --------------- |
| id           | int *自动增量*                             | 自增ID          |
| rack_id      | int *NULL* [**0**]                         | 机柜            |
| enclosure_id | int *NULL* [**0**]                         | 机位            |
| nb_u         | int *NULL*                                 | 高度            |
| managementip | varchar(255) *NULL* []                     | 管理IP，IP 地址 |
| powera_id    | int *NULL* [**0**]                         | 电源A           |
| powerB_id    | int *NULL* [**0**]                         | 电源B           |
| redundancy   | varchar(20) *NULL* [**1**]                 | 冗余            |
| finalclass   | varchar(255) *NULL* [**DatacenterDevice**] | 二级配置项      |

### 索引

| PRIMARY | *id*             |
| :------ | ---------------- |
| INDEX   | *rack_id*        |
| INDEX   | *enclosure_id*   |
| INDEX   | *powera_id*      |
| INDEX   | *powerB_id*      |
| INDEX   | *finalclass*(95) |