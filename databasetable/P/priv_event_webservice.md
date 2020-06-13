priv_event_webservice

Web service event (EventWebService) - Trace of an web service call

日志事件 (Event) >> EventWebService

| 列          | 类型                      | 注释     |
| :---------- | ------------------------- | -------- |
| id          | int *自动增量*            | 自增ID   |
| verb        | varchar(255) *NULL* []    | Verb     |
| result      | tinyint(1) *NULL* [**0**] | Result   |
| log_info    | text *NULL*               | 信息日志 |
| log_warning | text *NULL*               | 警告日志 |
| log_error   | text *NULL*               | 错误日志 |
| data        | text *NULL*               | 数据     |

### 索引

| PRIMARY | *id* |
| :------ | ---- |
|         |      |