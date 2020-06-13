databaseschema

功能配置项 (FunctionalCI) >> DatabaseSchema

数据库

| 列          | 类型               | 注释                                        |
| :---------- | ------------------ | ------------------------------------------- |
| id          | int *自动增量*     | 自增ID                                      |
| dbserver_id | int *NULL* [**0**] | 数据库服务器，数据库服务器 (DBServer)的外键 |

### 索引

| PRIMARY | *id*          |
| :------ | ------------- |
| INDEX   | *dbserver_id* |