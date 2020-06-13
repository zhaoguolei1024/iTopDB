priv_link_action_trigger

操作/触发器 (lnkTriggerAction) - Link between a trigger and an action



| 列         | 类型               | 注释   |
| :--------- | ------------------ | ------ |
| link_id    | int *自动增量*     | 自增ID |
| action_id  | int *NULL* [**0**] | 操作   |
| trigger_id | int *NULL* [**0**] | 触发器 |
| order      | int *NULL* [**0**] | 顺序   |

### 索引

| PRIMARY | *link_id*    |
| :------ | ------------ |
| INDEX   | *action_id*  |
| INDEX   | *trigger_id* |