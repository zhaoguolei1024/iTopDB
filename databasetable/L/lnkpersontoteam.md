lnkpersontoteam

链接 个体 / 团队 (lnkPersonToTeam)



| 列        | 类型               | 注释   |
| :-------- | ------------------ | ------ |
| id        | int *自动增量*     | 自增ID |
| team_id   | int *NULL* [**0**] | 团队   |
| person_id | int *NULL* [**0**] | 个体   |
| role_id   | int *NULL* [**0**] | 角色   |

### 索引

| PRIMARY | *id*        |
| :------ | ----------- |
| INDEX   | *team_id*   |
| INDEX   | *person_id* |
| INDEX   | *role_id*   |