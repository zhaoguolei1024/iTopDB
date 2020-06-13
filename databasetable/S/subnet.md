subnet

子网 (Subnet)



| 列          | 类型                   | 注释     |
| :---------- | ---------------------- | -------- |
| id          | int *自动增量*         | 自增ID   |
| description | text *NULL*            | 描述     |
| subnet_name | varchar(255) *NULL* [] | 子网名称 |
| org_id      | int *NULL* [**0**]     | 组织ID   |
| ip          | varchar(255) *NULL* [] | IP       |
| ip_mask     | varchar(255) *NULL* [] | 掩码     |

### 索引

| PRIMARY | *id*          |
| :------ | ------------- |
| INDEX   | *org_id*      |
| INDEX   | *ip*(95)      |
| INDEX   | *ip_mask*(95) |