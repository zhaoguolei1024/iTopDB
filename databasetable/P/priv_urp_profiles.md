priv_urp_profiles

角色 (URP_Profiles) - 用户角色





| 列          | 类型                   | 注释   |
| :---------- | ---------------------- | ------ |
| id          | int *自动增量*         | 自增ID |
| name        | varchar(255) *NULL* [] | 名称   |
| description | varchar(255) *NULL* [] | 描述   |

### 索引

| PRIMARY | *id*       |
| :------ | ---------- |
| INDEX   | *name*(95) |