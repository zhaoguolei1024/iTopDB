| 列                    | 类型                                                    | 注释 |
| :-------------------- | ------------------------------------------------------- | ---- |
| id                    | int [**0**]                                             |      |
| primary_key           | varchar(255) *NULL*                                     |      |
| contactid             | varchar(255) *NULL*                                     |      |
| login                 | varchar(255) *NULL*                                     |      |
| language              | varchar(255) *NULL*                                     |      |
| status                | enum('disabled','enabled') *NULL*                       |      |
| profile_list          | text *NULL*                                             |      |
| allowed_org_list      | text *NULL*                                             |      |
| reset_pwd_token       | tinytext *NULL*                                         |      |
| password              | tinytext *NULL*                                         |      |
| expiration            | enum('can_expire','force_expire','never_expire') *NULL* |      |
| password_renewed_date | varchar(10) *NULL*                                      |      |

### 索引

| INDEX | *id*          |
| :---- | ------------- |
| INDEX | *primary_key* |