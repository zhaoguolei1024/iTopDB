sla

SLA (SLA)



| 列          | 类型                   | 注释   |
| :---------- | ---------------------- | ------ |
| id          | int *自动增量*         | 自增ID |
| name        | varchar(255) *NULL* [] | 名称   |
| description | text *NULL*            | 描述   |
| org_id      | int *NULL* [**0**]     | 组织ID |

### 索引

| PRIMARY | *id*       |
| :------ | ---------- |
| INDEX   | *name*(95) |
| INDEX   | *org_id*   |