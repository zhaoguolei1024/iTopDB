priv_urp_userorg

用户组织 (URP_UserOrg) - 可以访问的组织



| 列             | 类型                   | 注释       |
| :------------- | ---------------------- | ---------- |
| id             | int *自动增量*         | 自增ID     |
| userid         | int *NULL* [**0**]     | 用户       |
| allowed_org_id | int *NULL* [**0**]     | 可访问组织 |
| reason         | varchar(255) *NULL* [] | 原因       |

### 索引

| PRIMARY | *id*             |
| :------ | ---------------- |
| INDEX   | *userid*         |
| INDEX   | *allowed_org_id* |