lnkgrouptoci

链接 配置组 / 配置项 (lnkGroupToCI)



| 列       | 类型                   | 注释   |
| :------- | ---------------------- | ------ |
| id       | int *自动增量*         | 自增ID |
| group_id | int *NULL* [**0**]     | 组     |
| ci_id    | int *NULL* [**0**]     | 配置项 |
| reason   | varchar(255) *NULL* [] | 原因   |

### 索引

| PRIMARY | *id*       |
| :------ | ---------- |
| INDEX   | *group_id* |
| INDEX   | *ci_id*    |