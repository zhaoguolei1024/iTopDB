softwareinstance

软件实例 (SoftwareInstance)

功能配置项 (FunctionalCI) >> SoftwareInstance

| 列                 | 类型                                       | 注释                                 |
| :----------------- | ------------------------------------------ | ------------------------------------ |
| id                 | int *自动增量*                             | 自增ID                               |
| functionalci_id    | int *NULL* [**0**]                         | 配置项ID                             |
| software_id        | int *NULL* [**0**]                         | 软件ID                               |
| softwarelicence_id | int *NULL* [**0**]                         | 软件许可证ID                         |
| path               | varchar(255) *NULL* []                     | 路径                                 |
| status             | enum('active','inactive') *NULL*           | 状态，启用 (active), 停用 (inactive) |
| finalclass         | varchar(255) *NULL* [**SoftwareInstance**] | 二级配置项                           |

### 索引

| PRIMARY | *id*                 |
| :------ | -------------------- |
| INDEX   | *functionalci_id*    |
| INDEX   | *software_id*        |
| INDEX   | *softwarelicence_id* |
| INDEX   | *finalclass*(95)     |