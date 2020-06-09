| 列           | 类型                                      | 注释 |
| :----------- | ----------------------------------------- | ---- |
| id           | int *自动增量*                            |      |
| name         | varchar(255) *NULL* []                    |      |
| priority     | enum('1','2','3','4') *NULL*              |      |
| request_type | enum('incident','service_request') *NULL* |      |
| metric       | enum('tto','ttr') *NULL*                  |      |
| value        | int *NULL*                                |      |
| unit         | enum('hours','minutes') *NULL*            |      |

### 索引

| PRIMARY | *id*       |
| :------ | ---------- |
| INDEX   | *name*(95) |