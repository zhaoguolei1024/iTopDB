| 列           | 类型                    | 注释 |
| :----------- | ----------------------- | ---- |
| id           | int *自动增量*          |      |
| webserver_id | int *NULL* [**0**]      |      |
| url          | varchar(2048) *NULL* [] |      |

### 索引

| PRIMARY | *id*           |
| :------ | -------------- |
| INDEX   | *webserver_id* |