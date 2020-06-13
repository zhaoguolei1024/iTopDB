lnkvirtualdevicetovolume

链接 虚拟设备 / 逻辑卷 (lnkVirtualDeviceToVolume)



| 列               | 类型                   | 注释     |
| :--------------- | ---------------------- | -------- |
| id               | int *自动增量*         | 自增ID   |
| volume_id        | int *NULL* [**0**]     | 逻辑卷   |
| virtualdevice_id | int *NULL* [**0**]     | 虚拟设备 |
| size_used        | varchar(255) *NULL* [] | 已用容量 |

### 索引

| PRIMARY | *id*               |
| :------ | ------------------ |
| INDEX   | *volume_id*        |
| INDEX   | *virtualdevice_id* |