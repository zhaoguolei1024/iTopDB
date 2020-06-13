priv_async_task

异步任务 (AsyncTask)





| 列                | 类型                                                         | 注释                                                         |
| :---------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| id                | int *自动增量*                                               | 自增ID                                                       |
| status            | enum('error','idle','planned','running') *NULL* [**planned**] | 状态，错误的(error), 闲置的(idle), 有计划的 (planned), 运行中的(running) |
| created           | datetime *NULL*                                              | 已创建                                                       |
| started           | datetime *NULL*                                              | 已开始                                                       |
| planned           | datetime *NULL*                                              | 已计划                                                       |
| event_id          | int *NULL* [**0**]                                           | 事件                                                         |
| remaining_retries | int *NULL* [**0**]                                           | 剩余重试次数                                                 |
| last_error_code   | int *NULL* [**0**]                                           | 最后一个错误代码                                             |
| last_error        | varchar(255) *NULL* []                                       | 最后一个错误                                                 |
| last_attempt      | datetime *NULL*                                              | 最后一次尝试                                                 |
| realclass         | varchar(255) *NULL* [**AsyncTask**]                          | Final class                                                  |

### 索引

| PRIMARY | *id*            |
| :------ | --------------- |
| INDEX   | *created*       |
| INDEX   | *event_id*      |
| INDEX   | *realclass*(95) |