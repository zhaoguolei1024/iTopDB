| 列                 | 类型                                       | 注释 |
| :----------------- | ------------------------------------------ | ---- |
| id                 | int *自动增量*                             |      |
| functionalci_id    | int *NULL* [**0**]                         |      |
| software_id        | int *NULL* [**0**]                         |      |
| softwarelicence_id | int *NULL* [**0**]                         |      |
| path               | varchar(255) *NULL* []                     |      |
| status             | enum('active','inactive') *NULL*           |      |
| finalclass         | varchar(255) *NULL* [**SoftwareInstance**] |      |

### 索引

| PRIMARY | *id*                 |
| :------ | -------------------- |
| INDEX   | *functionalci_id*    |
| INDEX   | *software_id*        |
| INDEX   | *softwarelicence_id* |
| INDEX   | *finalclass*(95)     |