priv_sync_replica

Synchro Replica (SynchroReplica)

复制品

| 列                  | 类型                                                         | 注释                                                         |
| :------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| id                  | int *自动增量*                                               | 自增ID                                                       |
| sync_source_id      | int *NULL* [**0**]                                           | 异步数据源                                                   |
| dest_id             | int *NULL* [**0**]                                           | 目标对象                                                     |
| dest_class          | varchar(255) *NULL* [**Organization**]                       | 目标分类                                                     |
| status_last_seen    | datetime *NULL*                                              | 最后查看时间                                                 |
| status              | enum('modified','new','obsolete','orphan','synchronized') *NULL* [**new**] | 状态，已修改 (modified), 新建 (new), 废弃 (obsolete), Orphan (orphan), 已同步 (synchronized) |
| status_dest_creator | tinyint(1) *NULL* [**0**]                                    | 状态目标创建者                                               |
| status_last_error   | varchar(255) *NULL* []                                       | 最后的错误                                                   |
| status_last_warning | varchar(255) *NULL* []                                       | 最后的警告                                                   |
| info_creation_date  | datetime *NULL*                                              | 创建日期                                                     |
| info_last_modified  | datetime *NULL*                                              | 最后修改日期                                                 |

### 索引

| PRIMARY | *id*                        |
| :------ | --------------------------- |
| INDEX   | *sync_source_id*            |
| INDEX   | *dest_class*(95)            |
| INDEX   | *dest_class*(95), *dest_id* |