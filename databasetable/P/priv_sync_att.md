priv_sync_att

同步属性 (SynchroAttribute)



| 列             | 类型                                                         | 注释                                                         |
| :------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| id             | int *自动增量*                                               | 自增ID                                                       |
| sync_source_id | int *NULL* [**0**]                                           | 同步数据源                                                   |
| attcode        | varchar(255) *NULL* []                                       | 属性代码                                                     |
| update         | tinyint(1) *NULL* [**1**]                                    | 更新                                                         |
| reconcile      | tinyint(1) *NULL* [**0**]                                    | 一致                                                         |
| update_policy  | enum('master_locked','master_unlocked','write_if_empty') *NULL* [**master_locked**] | 更新策略，加锁 (master_locked), 解锁 (master_unlocked), 如果为空则初始化 (write_if_empty) |
| finalclass     | varchar(255) *NULL* [**SynchroAttribute**]                   | 类别                                                         |

### 索引

| PRIMARY | *id*             |
| :------ | ---------------- |
| INDEX   | *sync_source_id* |
| INDEX   | *attcode*(95)    |
| INDEX   | *finalclass*(95) |