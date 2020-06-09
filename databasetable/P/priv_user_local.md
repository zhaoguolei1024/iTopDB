| 列                    | 类型                                                         | 注释 |
| :-------------------- | ------------------------------------------------------------ | ---- |
| id                    | int *自动增量*                                               |      |
| password_hash         | tinyblob *NULL*                                              |      |
| password_salt         | tinyblob *NULL*                                              |      |
| expiration            | enum('can_expire','force_expire','never_expire') *NULL* [**never_expire**] |      |
| password_renewed_date | date *NULL*                                                  |      |

### 索引

| PRIMARY | *id* |
| :------ | ---- |
|         |      |