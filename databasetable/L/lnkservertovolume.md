lnkservertovolume

链接 服务器 / 逻辑卷 (lnkServerToVolume)



| 列        | 类型                   | 注释     |
| :-------- | ---------------------- | -------- |
| id        | int *自动增量*         | 自增ID   |
| volume_id | int *NULL* [**0**]     | 逻辑卷   |
| server_id | int *NULL* [**0**]     | 服务器   |
| size_used | varchar(255) *NULL* [] | 已用容量 |

### 索引

| PRIMARY | *id*        |
| :------ | ----------- |
| INDEX   | *volume_id* |
| INDEX   | *server_id* |