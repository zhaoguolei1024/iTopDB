| 列                                     | 类型                                                     | 注释 |
| :------------------------------------- | -------------------------------------------------------- | ---- |
| id                                     | int *自动增量*                                           |      |
| sync_source_id                         | int *NULL* [**0**]                                       |      |
| start_date                             | datetime *NULL*                                          |      |
| end_date                               | datetime *NULL*                                          |      |
| status                                 | enum('completed','error','running') *NULL* [**running**] |      |
| status_curr_job                        | int *NULL* [**0**]                                       |      |
| status_curr_pos                        | int *NULL* [**0**]                                       |      |
| stats_nb_replica_seen                  | int *NULL* [**0**]                                       |      |
| stats_nb_replica_total                 | int *NULL* [**0**]                                       |      |
| stats_nb_obj_deleted                   | int *NULL* [**0**]                                       |      |
| stats_deleted_errors                   | int *NULL* [**0**]                                       |      |
| stats_nb_obj_obsoleted                 | int *NULL* [**0**]                                       |      |
| stats_nb_obj_obsoleted_errors          | int *NULL* [**0**]                                       |      |
| stats_nb_obj_created                   | int *NULL* [**0**]                                       |      |
| stats_nb_obj_created_errors            | int *NULL* [**0**]                                       |      |
| stats_nb_obj_created_warnings          | int *NULL* [**0**]                                       |      |
| stats_nb_obj_updated                   | int *NULL* [**0**]                                       |      |
| stats_nb_obj_updated_errors            | int *NULL* [**0**]                                       |      |
| stats_nb_obj_updated_warnings          | int *NULL* [**0**]                                       |      |
| stats_nb_obj_unchanged_warnings        | int *NULL* [**0**]                                       |      |
| stats_nb_replica_reconciled_errors     | int *NULL* [**0**]                                       |      |
| stats_nb_replica_disappeared_no_action | int *NULL* [**0**]                                       |      |
| stats_nb_obj_new_updated               | int *NULL* [**0**]                                       |      |
| stats_nb_obj_new_updated_warnings      | int *NULL* [**0**]                                       |      |
| stats_nb_obj_new_unchanged             | int *NULL* [**0**]                                       |      |
| stats_nb_obj_new_unchanged_warnings    | int *NULL* [**0**]                                       |      |
| last_error                             | text *NULL*                                              |      |
| traces                                 | longtext *NULL*                                          |      |
| memory_usage_peak                      | int *NULL* [**0**]                                       |      |

### 索引

| PRIMARY | *id*             |
| :------ | ---------------- |
| INDEX   | *sync_source_id* |