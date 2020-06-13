priv_user

用户 (User) - 用户登录名



| 列         | 类型                                            | 注释                                  |
| :--------- | ----------------------------------------------- | ------------------------------------- |
| id         | int *自动增量*                                  | 自增ID                                |
| contactid  | int *NULL* [**0**]                              | 联系人ID                              |
| login      | varchar(255) *NULL* []                          | 登录名                                |
| language   | varchar(255) *NULL* [**EN US**]                 | 语言                                  |
| status     | enum('disabled','enabled') *NULL* [**enabled**] | 状态，停用 (disabled), 启用 (enabled) |
| finalclass | varchar(255) *NULL* [**User**]                  | 帐户类别                              |

### 索引

| PRIMARY | *id*             |
| :------ | ---------------- |
| INDEX   | *contactid*      |
| INDEX   | *login*(95)      |
| INDEX   | *language*(95)   |
| INDEX   | *finalclass*(95) |