synchro_data_userlocal_2

同步数据源 (SynchroDataSource)

| 列                    | 类型                                                    | 注释             |
| :-------------------- | ------------------------------------------------------- | ---------------- |
| id                    | int [**0**]                                             | 自增ID           |
| primary_key           | varchar(255) *NULL*                                     | 主键             |
| contactid             | varchar(255) *NULL*                                     | 联系人ID         |
| login                 | varchar(255) *NULL*                                     | 登录名           |
| language              | varchar(255) *NULL*                                     | 语言             |
| status                | enum('disabled','enabled') *NULL*                       | 状态，启用，停用 |
| profile_list          | text *NULL*                                             | 权限列表         |
| allowed_org_list      | text *NULL*                                             | 可用组织         |
| reset_pwd_token       | tinytext *NULL*                                         | 重置密码token    |
| password              | tinytext *NULL*                                         | 密码             |
| expiration            | enum('can_expire','force_expire','never_expire') *NULL* | 过期             |
| password_renewed_date | varchar(10) *NULL*                                      | 更新密码时间     |

### 索引

| INDEX | *id*          |
| :---- | ------------- |
| INDEX | *primary_key* |