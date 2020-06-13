pc

PC (PC)

功能配置项 (FunctionalCI) >> 物理设备 (PhysicalDevice) >> 可连接的配置项 (ConnectableCI) >> PC



| 列           | 类型                            | 注释                                    |
| :----------- | ------------------------------- | --------------------------------------- |
| id           | int *自动增量*                  | 自增ID                                  |
| osfamily_id  | int *NULL* [**0**]              | 操作系统家族                            |
| osversion_id | int *NULL* [**0**]              | 操作系统版本                            |
| cpu          | varchar(255) *NULL* []          | CPU                                     |
| ram          | varchar(255) *NULL* []          | 内存                                    |
| type         | enum('desktop','laptop') *NULL* | 类型，桌面型 (desktop), 笔记本 (laptop) |

### 索引

| PRIMARY | *id*           |
| :------ | -------------- |
| INDEX   | *osfamily_id*  |
| INDEX   | *osversion_id* |