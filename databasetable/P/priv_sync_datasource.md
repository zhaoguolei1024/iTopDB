| 列                      | 类型                                                         | 注释 |
| :---------------------- | ------------------------------------------------------------ | ---- |
| id                      | int *自动增量*                                               |      |
| name                    | varchar(255) *NULL* []                                       |      |
| description             | text *NULL*                                                  |      |
| status                  | enum('implementation','obsolete','production') *NULL* [**implementation**] |      |
| user_id                 | int *NULL* [**0**]                                           |      |
| notify_contact_id       | int *NULL* [**0**]                                           |      |
| scope_class             | varchar(255) *NULL* [**TagSetFieldDataFor_FAQ__domains**]    |      |
| database_table_name     | varchar(255) *NULL* []                                       |      |
| scope_restriction       | varchar(255) *NULL* []                                       |      |
| full_load_periodicity   | int unsigned *NULL*                                          |      |
| reconciliation_policy   | enum('use_attributes','use_primary_key') *NULL* [**use_attributes**] |      |
| action_on_zero          | enum('create','error') *NULL* [**create**]                   |      |
| action_on_one           | enum('error','update') *NULL* [**update**]                   |      |
| action_on_multiple      | enum('create','error','take_first') *NULL* [**error**]       |      |
| delete_policy           | enum('delete','ignore','update','update_then_delete') *NULL* [**ignore**] |      |
| delete_policy_update    | varchar(255) *NULL* []                                       |      |
| delete_policy_retention | int unsigned *NULL*                                          |      |
| user_delete_policy      | enum('administrators','everybody','nobody') *NULL* [**nobody**] |      |
| url_icon                | varchar(2048) *NULL* []                                      |      |
| url_application         | varchar(255) *NULL* []                                       |      |

### 索引

| PRIMARY | *id*                |
| :------ | ------------------- |
| INDEX   | *name*(95)          |
| INDEX   | *user_id*           |
| INDEX   | *notify_contact_id* |
| INDEX   | *scope_class*(95)   |