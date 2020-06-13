priv_user_local

本地用户

用户 (User) >> 内部用户 (UserInternal) >> UserLocal



| 列                    | 类型                                                         | 注释                                                         |
| :-------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| id                    | int *自动增量*                                               | 自增ID                                                       |
| password_hash         | tinyblob *NULL*                                              | 密码hash                                                     |
| password_salt         | tinyblob *NULL*                                              | 密码salt                                                     |
| expiration            | enum('can_expire','force_expire','never_expire') *NULL* [**never_expire**] | 密码过期，允许过期 (can_expire), 已过期 (force_expire), 永不过期 (never_expire) |
| password_renewed_date | date *NULL*                                                  | 密码更新                                                     |

### 索引

| PRIMARY | *id* |
| :------ | ---- |
|         |      |