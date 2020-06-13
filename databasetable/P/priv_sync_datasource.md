priv_sync_datasource

同步数据源 (SynchroDataSource)



| 列                      | 类型                                                         | 注释                                                         |
| :---------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| id                      | int *自动增量*                                               | 自增ID                                                       |
| name                    | varchar(255) *NULL* []                                       | 名称                                                         |
| description             | text *NULL*                                                  | 描述                                                         |
| status                  | enum('implementation','obsolete','production') *NULL* [**implementation**] | 状态，上线 (implementation), 废弃 (obsolete), 生产 (production) |
| user_id                 | int *NULL* [**0**]                                           | 用户                                                         |
| notify_contact_id       | int *NULL* [**0**]                                           | 要通知的人                                                   |
| scope_class             | varchar(255) *NULL* [**TagSetFieldDataFor_FAQ__domains**]    | 目标类                                                       |
| database_table_name     | varchar(255) *NULL* []                                       | 数据库表名                                                   |
| scope_restriction       | varchar(255) *NULL* []                                       | 范围限制                                                     |
| full_load_periodicity   | int unsigned *NULL*                                          | 满载间隔                                                     |
| reconciliation_policy   | enum('use_attributes','use_primary_key') *NULL* [**use_attributes**] | 调节政策，use_attributes，use_primary_key                    |
| action_on_zero          | enum('create','error') *NULL* [**create**]                   | 执行结果成功时                                               |
| action_on_one           | enum('error','update') *NULL* [**update**]                   | 执行结果失败时                                               |
| action_on_multiple      | enum('create','error','take_first') *NULL* [**error**]       | 执行结果未知时                                               |
| delete_policy           | enum('delete','ignore','update','update_then_delete') *NULL* [**ignore**] | 删除策略，删除 (delete), 忽略 (ignore), 更新 (update), 先更新再删除 (update_then_delete) |
| delete_policy_update    | varchar(255) *NULL* []                                       | 更新规则                                                     |
| delete_policy_retention | int unsigned *NULL*                                          | 保留期限                                                     |
| user_delete_policy      | enum('administrators','everybody','nobody') *NULL* [**nobody**] | 授权用户，仅限管理员 (administrators), Everybody allowed to delete such objects (everybody), Nobody (nobody) |
| url_icon                | varchar(2048) *NULL* []                                      | 图标的超链接                                                 |
| url_application         | varchar(255) *NULL* []                                       | 应用的超链接                                                 |

### 索引

| PRIMARY | *id*                |
| :------ | ------------------- |
| INDEX   | *name*(95)          |
| INDEX   | *user_id*           |
| INDEX   | *notify_contact_id* |
| INDEX   | *scope_class*(95)   |