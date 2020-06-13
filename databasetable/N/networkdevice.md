networkdevice

网络设备 (NetworkDevice)

功能配置项 (FunctionalCI) >> 物理设备 (PhysicalDevice) >> 可连接的配置项 (ConnectableCI) >> 数据中心设备 (DatacenterDevice) >> NetworkDevice



| 列                   | 类型                   | 注释         |
| :------------------- | ---------------------- | ------------ |
| id                   | int *自动增量*         | 自增ID       |
| networkdevicetype_id | int *NULL* [**0**]     | 网络设备类型 |
| iosversion_id        | int *NULL* [**0**]     | IOS 版本     |
| ram                  | varchar(255) *NULL* [] | 内存         |

### 索引

| PRIMARY | *id*                   |
| :------ | ---------------------- |
| INDEX   | *networkdevicetype_id* |
| INDEX   | *iosversion_id*        |