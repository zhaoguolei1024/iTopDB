virtualdevice

虚拟设备 (VirtualDevice)

功能配置项 (FunctionalCI) >> VirtualDevice



| 列         | 类型                                                         | 注释                                                         |
| :--------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| id         | int *自动增量*                                               | 自增ID                                                       |
| status     | enum('implementation','obsolete','production','stock') *NULL* [**production**] | 状态，上线 (implementation), 废弃 (obsolete), 生产 (production), 闲置 (stock) |
| finalclass | varchar(255) *NULL* [**VirtualDevice**]                      | 二级配置项                                                   |

### 索引

| PRIMARY | *id*             |
| :------ | ---------------- |
| INDEX   | *finalclass*(95) |