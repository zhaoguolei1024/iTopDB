priv_urp_userprofile

角色目标用户 (URP_UserProfile) - 用户的角色





| 列          | 类型                   | 注释   |
| :---------- | ---------------------- | ------ |
| id          | int *自动增量*         | 自增ID |
| userid      | int *NULL* [**0**]     | 用户   |
| profileid   | int *NULL* [**0**]     | 角色   |
| description | varchar(255) *NULL* [] | 描述   |

### 索引

| PRIMARY | *id*        |
| :------ | ----------- |
| INDEX   | *userid*    |
| INDEX   | *profileid* |