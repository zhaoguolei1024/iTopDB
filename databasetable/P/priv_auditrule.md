priv_auditrule

审计规则 (AuditRule) - 用于检查指定审计类别的规则



| 列          | 类型                                   | 注释                                  |
| :---------- | -------------------------------------- | ------------------------------------- |
| id          | int *自动增量*                         | 自增ID                                |
| name        | varchar(255) *NULL* []                 | 名称                                  |
| description | varchar(255) *NULL* []                 | 审计规则描述                          |
| query       | text *NULL*                            | 要运行的查询                          |
| valid_flag  | enum('false','true') *NULL* [**true**] | 是否有效?，false (false), true (true) |
| category_id | int *NULL* [**0**]                     | 类别                                  |

### 索引

| PRIMARY | *id*          |
| :------ | ------------- |
| INDEX   | *name*(95)    |
| INDEX   | *category_id* |