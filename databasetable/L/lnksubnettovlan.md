lnksubnettovlan

链接 子网 / VLAN (lnkSubnetToVLAN)



| 列        | 类型               | 注释   |
| :-------- | ------------------ | ------ |
| id        | int *自动增量*     | 自增ID |
| subnet_id | int *NULL* [**0**] | 子网   |
| vlan_id   | int *NULL* [**0**] | VLAN   |

### 索引

| PRIMARY | *id*        |
| :------ | ----------- |
| INDEX   | *subnet_id* |
| INDEX   | *vlan_id*   |