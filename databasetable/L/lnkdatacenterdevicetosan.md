lnkdatacenterdevicetosan

链接 SAN / 数据中心设备 (lnkSanToDatacenterDevice)



| 列                    | 类型                   | 注释       |
| :-------------------- | ---------------------- | ---------- |
| id                    | int *自动增量*         | 自增ID     |
| san_id                | int *NULL* [**0**]     | SAN 交换机 |
| datacenterdevice_id   | int *NULL* [**0**]     | 设备       |
| san_port              | varchar(255) *NULL* [] | SAN fc     |
| datacenterdevice_port | varchar(255) *NULL* [] | Device fc  |

### 索引

| PRIMARY | *id*                  |
| :------ | --------------------- |
| INDEX   | *san_id*              |
| INDEX   | *datacenterdevice_id* |



注：lnkdatacenterdevicetosan与lnkSanToDatacenterDevice 不一样

