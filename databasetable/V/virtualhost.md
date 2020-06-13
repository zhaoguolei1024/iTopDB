virtualhost

宿主机 (VirtualHost)

功能配置项 (FunctionalCI) >> 虚拟设备 (VirtualDevice) >> VirtualHost



| 列         | 类型                                  | 注释   |
| :--------- | ------------------------------------- | ------ |
| id         | int *自动增量*                        | 自增ID |
| finalclass | varchar(255) *NULL* [**VirtualHost**] | 子类别 |

### 索引

| PRIMARY | *id*             |
| :------ | ---------------- |
| INDEX   | *finalclass*(95) |