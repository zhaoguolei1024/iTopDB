| 列                   | 类型                                        | 注释 |
| :------------------- | ------------------------------------------- | ---- |
| id                   | int *自动增量*                              |      |
| class_name           | varchar(255) *NULL* []                      |      |
| first_run_date       | datetime *NULL*                             |      |
| latest_run_date      | datetime *NULL*                             |      |
| next_run_date        | datetime *NULL*                             |      |
| total_exec_count     | int *NULL* [**0**]                          |      |
| latest_run_duration  | decimal(8,3) *NULL* [**0.000**]             |      |
| min_run_duration     | decimal(8,3) *NULL* [**0.000**]             |      |
| max_run_duration     | decimal(8,3) *NULL* [**0.000**]             |      |
| average_run_duration | decimal(8,3) *NULL* [**0.000**]             |      |
| running              | tinyint(1) *NULL* [**0**]                   |      |
| status               | enum('active','paused') *NULL* [**active**] |      |
| system_user          | varchar(255) *NULL* []                      |      |

### 索引

| PRIMARY | *id*             |
| :------ | ---------------- |
| INDEX   | *class_name*(95) |