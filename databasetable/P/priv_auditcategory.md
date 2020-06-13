priv_auditcategory

审计类别 (AuditCategory) - 全部审计中的一个区段



| 列             | 类型                   | 注释         |
| :------------- | ---------------------- | ------------ |
| id             | int *自动增量*         | 自增ID       |
| name           | varchar(255) *NULL* [] | 类别名称     |
| description    | varchar(255) *NULL* [] | 审计类别描述 |
| definition_set | text *NULL*            | 定义         |

### 索引

| PRIMARY | *id*       |
| :------ | ---------- |
| INDEX   | *name*(95) |