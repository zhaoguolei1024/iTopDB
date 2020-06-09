| 列             | 类型                   | 注释 |
| :------------- | ---------------------- | ---- |
| id             | int *自动增量*         |      |
| virtualhost_id | int *NULL* [**0**]     |      |
| osfamily_id    | int *NULL* [**0**]     |      |
| osversion_id   | int *NULL* [**0**]     |      |
| oslicence_id   | int *NULL* [**0**]     |      |
| cpu            | varchar(255) *NULL* [] |      |
| ram            | varchar(255) *NULL* [] |      |
| managementip   | varchar(255) *NULL* [] |      |

### 索引

| PRIMARY | *id*             |
| :------ | ---------------- |
| INDEX   | *virtualhost_id* |
| INDEX   | *osfamily_id*    |
| INDEX   | *osversion_id*   |
| INDEX   | *oslicence_id*   |