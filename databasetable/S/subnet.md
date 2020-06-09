| 列          | 类型                   | 注释 |
| :---------- | ---------------------- | ---- |
| id          | int *自动增量*         |      |
| description | text *NULL*            |      |
| subnet_name | varchar(255) *NULL* [] |      |
| org_id      | int *NULL* [**0**]     |      |
| ip          | varchar(255) *NULL* [] |      |
| ip_mask     | varchar(255) *NULL* [] |      |

### 索引

| PRIMARY | *id*          |
| :------ | ------------- |
| INDEX   | *org_id*      |
| INDEX   | *ip*(95)      |
| INDEX   | *ip_mask*(95) |