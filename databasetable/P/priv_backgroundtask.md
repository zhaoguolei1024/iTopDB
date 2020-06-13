priv_backgroundtask

后台任务 (BackgroundTask)



| 列                   | 类型                                        | 注释                                   |
| :------------------- | ------------------------------------------- | -------------------------------------- |
| id                   | int *自动增量*                              | 自增ID                                 |
| class_name           | varchar(255) *NULL* []                      | 类名                                   |
| first_run_date       | datetime *NULL*                             | 首次运行时间                           |
| latest_run_date      | datetime *NULL*                             | 最近运行时间                           |
| next_run_date        | datetime *NULL*                             | 下次运行时间                           |
| total_exec_count     | int *NULL* [**0**]                          | 一共执行的次数                         |
| latest_run_duration  | decimal(8,3) *NULL* [**0.000**]             | 最近运行时长                           |
| min_run_duration     | decimal(8,3) *NULL* [**0.000**]             | 最少运行时长                           |
| max_run_duration     | decimal(8,3) *NULL* [**0.000**]             | 最多运行时长                           |
| average_run_duration | decimal(8,3) *NULL* [**0.000**]             | 平均运行时长                           |
| running              | tinyint(1) *NULL* [**0**]                   | 运行中                                 |
| status               | enum('active','paused') *NULL* [**active**] | 状态，active (active), paused (paused) |
| system_user          | varchar(255) *NULL* []                      | 系统用户账户                           |

### 索引

| PRIMARY | *id*             |
| :------ | ---------------- |
| INDEX   | *class_name*(95) |