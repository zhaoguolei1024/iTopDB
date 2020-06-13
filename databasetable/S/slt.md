slt

SLT (SLT)

| 列           | 类型                                      | 注释                                                  |
| :----------- | ----------------------------------------- | ----------------------------------------------------- |
| id           | int *自动增量*                            | 自增ID                                                |
| name         | varchar(255) *NULL* []                    | 名称                                                  |
| priority     | enum('1','2','3','4') *NULL*              | 优先级，非常高 (1), 高 (2), 中 (3), 低 (4)            |
| request_type | enum('incident','service_request') *NULL* | 需求类型，事件 (incident), 服务需求 (service_request) |
| metric       | enum('tto','ttr') *NULL*                  | 指标，响应时间 (tto), 解决时间 (ttr)                  |
| value        | int *NULL*                                | 值                                                    |
| unit         | enum('hours','minutes') *NULL*            | 单位，小时 (hours), 分钟 (minutes)                    |

### 索引

| PRIMARY | *id*       |
| :------ | ---------- |
| INDEX   | *name*(95) |