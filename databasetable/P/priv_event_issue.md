priv_event_issue

Issue event (EventIssue) - Trace of an issue (warning, error, etc.)

日志事件 (Event) >> EventIssue



| 列             | 类型                   | 注释      |
| :------------- | ---------------------- | --------- |
| id             | int *自动增量*         | ID        |
| issue          | varchar(255) *NULL* [] | 事件      |
| impact         | varchar(255) *NULL* [] | 影响      |
| page           | varchar(255) *NULL* [] | 页面      |
| arguments_post | longtext *NULL*        | post 参数 |
| arguments_get  | longtext *NULL*        | get 参数  |
| callstack      | longtext *NULL*        | 回调函数  |
| data           | longtext *NULL*        | 数据      |

### 索引

| PRIMARY | *id* |
| :------ | ---- |
|         |      |