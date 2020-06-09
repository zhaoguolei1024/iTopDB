| 列             | 类型                                                         | 注释 |
| :------------- | ------------------------------------------------------------ | ---- |
| id             | int *自动增量*                                               |      |
| sync_source_id | int *NULL* [**0**]                                           |      |
| attcode        | varchar(255) *NULL* []                                       |      |
| update         | tinyint(1) *NULL* [**1**]                                    |      |
| reconcile      | tinyint(1) *NULL* [**0**]                                    |      |
| update_policy  | enum('master_locked','master_unlocked','write_if_empty') *NULL* [**master_locked**] |      |
| finalclass     | varchar(255) *NULL* [**SynchroAttribute**]                   |      |

### 索引

| PRIMARY | *id*             |
| :------ | ---------------- |
| INDEX   | *sync_source_id* |
| INDEX   | *attcode*(95)    |
| INDEX   | *finalclass*(95) |