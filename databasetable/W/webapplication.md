webapplication

Web 应用 (WebApplication)

功能配置项 (FunctionalCI) >> WebApplication



| 列           | 类型                    | 注释       |
| :----------- | ----------------------- | ---------- |
| id           | int *自动增量*          | 自增ID     |
| webserver_id | int *NULL* [**0**]      | Web 服务器 |
| url          | varchar(2048) *NULL* [] | URL        |

### 索引

| PRIMARY | *id*           |
| :------ | -------------- |
| INDEX   | *webserver_id* |