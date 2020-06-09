| 列             | 类型                   | 注释 |
| :------------- | ---------------------- | ---- |
| id             | int *自动增量*         |      |
| userid         | int *NULL* [**0**]     |      |
| allowed_org_id | int *NULL* [**0**]     |      |
| reason         | varchar(255) *NULL* [] |      |

### 索引

| PRIMARY | *id*             |
| :------ | ---------------- |
| INDEX   | *userid*         |
| INDEX   | *allowed_org_id* |