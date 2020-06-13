powerconnection

电源连接 (PowerConnection)

功能配置项 (FunctionalCI) >> 物理设备 (PhysicalDevice) >> PowerConnection



| 列         | 类型                                      | 注释       |
| :--------- | ----------------------------------------- | ---------- |
| id         | int *自动增量*                            | 自增ID     |
| finalclass | varchar(255) *NULL* [**PowerConnection**] | 二级配置项 |

### 索引

| PRIMARY | *id*             |
| :------ | ---------------- |
| INDEX   | *finalclass*(95) |