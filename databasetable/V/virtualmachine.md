virtualmachine

虚拟机 (VirtualMachine)

功能配置项 (FunctionalCI) >> 虚拟设备 (VirtualDevice) >> VirtualMachine



| 列             | 类型                   | 注释           |
| :------------- | ---------------------- | -------------- |
| id             | int *自动增量*         | 自增ID         |
| virtualhost_id | int *NULL* [**0**]     | 宿主机         |
| osfamily_id    | int *NULL* [**0**]     | 操作系统家族   |
| osversion_id   | int *NULL* [**0**]     | 操作系统版本   |
| oslicence_id   | int *NULL* [**0**]     | 操作系统许可证 |
| cpu            | varchar(255) *NULL* [] | CPU            |
| ram            | varchar(255) *NULL* [] | 内存           |
| managementip   | varchar(255) *NULL* [] | 管理IP         |

### 索引

| PRIMARY | *id*             |
| :------ | ---------------- |
| INDEX   | *virtualhost_id* |
| INDEX   | *osfamily_id*    |
| INDEX   | *osversion_id*   |
| INDEX   | *oslicence_id*   |