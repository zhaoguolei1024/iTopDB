priv_event_restservice

REST/JSON 调用 (EventRestService) - Trace of a REST/JSON service call

日志事件 (Event) >> EventRestService



| 列          | 类型                   | 注释     |
| :---------- | ---------------------- | -------- |
| id          | int *自动增量*         | 自增ID   |
| operation   | varchar(255) *NULL* [] | 操作     |
| version     | varchar(255) *NULL* [] | 版本     |
| json_input  | text *NULL*            | 输入     |
| code        | int *NULL* [**0**]     | 代码     |
| json_output | text *NULL*            | 响应     |
| provider    | varchar(255) *NULL* [] | Provider |

### 索引

| PRIMARY | *id* |
| :------ | ---- |
|         |      |