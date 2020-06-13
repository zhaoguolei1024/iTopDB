priv_internaluser

内部用户 (UserInternal) - iTop 内部定义的用户

抽象类: 该类不能实例化对象.

用户 (User) >> UserInternal

| 列                   | 类型                                   | 注释     |
| :------------------- | -------------------------------------- | -------- |
| id                   | int *自动增量*                         | 自增ID   |
| reset_pwd_token_hash | tinyblob *NULL*                        | 密码hash |
| reset_pwd_token_salt | tinyblob *NULL*                        | 密码salt |
| finalclass           | varchar(255) *NULL* [**UserInternal**] | 帐户类别 |

### 索引

| PRIMARY | *id*             |
| :------ | ---------------- |
| INDEX   | *finalclass*(95) |