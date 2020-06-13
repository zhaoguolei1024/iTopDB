priv_app_dashboards

用户面板 (UserDashboard)



| 列        | 类型                   | 注释     |
| :-------- | ---------------------- | -------- |
| id        | int *自动增量*         | 自增ID   |
| user_id   | int *NULL* [**0**]     | 用户     |
| menu_code | varchar(255) *NULL* [] | 菜单代码 |
| contents  | text *NULL*            | 内容     |

### 索引

| PRIMARY | *id*      |
| :------ | --------- |
| INDEX   | *user_id* |