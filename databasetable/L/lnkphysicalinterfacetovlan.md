lnkphysicalinterfacetovlan

链接 物理网卡 / VLAN (lnkPhysicalInterfaceToVLAN)



| 列                   | 类型               | 注释     |
| :------------------- | ------------------ | -------- |
| id                   | int *自动增量*     | 自增ID   |
| physicalinterface_id | int *NULL* [**0**] | 物理网卡 |
| vlan_id              | int *NULL* [**0**] | VLAN     |

### 索引

| PRIMARY | *id*                   |
| :------ | ---------------------- |
| INDEX   | *physicalinterface_id* |
| INDEX   | *vlan_id*              |