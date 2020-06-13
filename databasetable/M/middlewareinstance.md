middlewareinstance

中间件实例 (MiddlewareInstance)

功能配置项 (FunctionalCI) >> MiddlewareInstance



| 列            | 类型               | 注释   |
| :------------ | ------------------ | ------ |
| id            | int *自动增量*     | 自增ID |
| middleware_id | int *NULL* [**0**] | 中间件 |

### 索引

| PRIMARY | *id*            |
| :------ | --------------- |
| INDEX   | *middleware_id* |