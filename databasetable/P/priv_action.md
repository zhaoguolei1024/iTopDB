

priv_action

自定义操作 (Action) - 用户定义的操作



| 列          | 类型                                                | 注释                                               |
| :---------- | --------------------------------------------------- | -------------------------------------------------- |
| id          | int *自动增量*                                      | 自增ID                                             |
| name        | varchar(255) *NULL* []                              | 名称                                               |
| description | varchar(255) *NULL* []                              | 描述                                               |
| status      | enum('test','enabled','disabled') *NULL* [**test**] | 状态测试 (test), 正式 (enabled), 停用 (disabled)， |
| realclass   | varchar(255) *NULL* [**Action**]                    |                                                    |

### 索引

| PRIMARY | *id*            |
| :------ | --------------- |
| INDEX   | *name*(95)      |
| INDEX   | *realclass*(95) |