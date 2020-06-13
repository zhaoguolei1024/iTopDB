priv_sync_log

同步日志 (SynchroLog)



| 列                                     | 类型                                                     | 注释                                                       |
| :------------------------------------- | -------------------------------------------------------- | ---------------------------------------------------------- |
| id                                     | int *自动增量*                                           | 自增ID                                                     |
| sync_source_id                         | int *NULL* [**0**]                                       | 同步数据源                                                 |
| start_date                             | datetime *NULL*                                          | 开始日期                                                   |
| end_date                               | datetime *NULL*                                          | 结束日期                                                   |
| status                                 | enum('completed','error','running') *NULL* [**running**] | 状态，已完成 (completed), 错误 (error), 正在运行 (running) |
| status_curr_job                        | int *NULL* [**0**]                                       | 当前工作状态                                               |
| status_curr_pos                        | int *NULL* [**0**]                                       | 当前位置状态                                               |
| stats_nb_replica_seen                  | int *NULL* [**0**]                                       | 已看到的副本                                               |
| stats_nb_replica_total                 | int *NULL* [**0**]                                       | 副本的数量                                                 |
| stats_nb_obj_deleted                   | int *NULL* [**0**]                                       | 已删除的对象                                               |
| stats_deleted_errors                   | int *NULL* [**0**]                                       | 删除的错误                                                 |
| stats_nb_obj_obsoleted                 | int *NULL* [**0**]                                       | 过时的统计数据                                             |
| stats_nb_obj_obsoleted_errors          | int *NULL* [**0**]                                       | 过时的统计数据的错误                                       |
| stats_nb_obj_created                   | int *NULL* [**0**]                                       | 创建的统计信息                                             |
| stats_nb_obj_created_errors            | int *NULL* [**0**]                                       | 创建的统计信息的错误                                       |
| stats_nb_obj_created_warnings          | int *NULL* [**0**]                                       | 统计数据创建警告                                           |
| stats_nb_obj_updated                   | int *NULL* [**0**]                                       | 统计数据更新                                               |
| stats_nb_obj_updated_errors            | int *NULL* [**0**]                                       | 统计数据更新错误                                           |
| stats_nb_obj_updated_warnings          | int *NULL* [**0**]                                       | 统计数据更新警告                                           |
| stats_nb_obj_unchanged_warnings        | int *NULL* [**0**]                                       | 统计数据对象未更改警告                                     |
| stats_nb_replica_reconciled_errors     | int *NULL* [**0**]                                       | 统计数据副本协调错误                                       |
| stats_nb_replica_disappeared_no_action | int *NULL* [**0**]                                       | 状态副本消失无动作                                         |
| stats_nb_obj_new_updated               | int *NULL* [**0**]                                       | 统计数据更新                                               |
| stats_nb_obj_new_updated_warnings      | int *NULL* [**0**]                                       | 统计数据更新警告                                           |
| stats_nb_obj_new_unchanged             | int *NULL* [**0**]                                       | 统计数据保持不变                                           |
| stats_nb_obj_new_unchanged_warnings    | int *NULL* [**0**]                                       | 统计数据保持不变警告                                       |
| last_error                             | text *NULL*                                              | 最后的错误                                                 |
| traces                                 | longtext *NULL*                                          | 踪迹                                                       |
| memory_usage_peak                      | int *NULL* [**0**]                                       | 内存使用高峰                                               |

### 索引

| PRIMARY | *id*             |
| :------ | ---------------- |
| INDEX   | *sync_source_id* |