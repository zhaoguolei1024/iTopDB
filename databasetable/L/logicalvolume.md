logicalvolume

逻辑卷 (LogicalVolume)



| 列                | 类型                   | 注释     |
| :---------------- | ---------------------- | -------- |
| id                | int *自动增量*         | 自增ID   |
| name              | varchar(255) *NULL* [] | 名称     |
| lun_id            | varchar(255) *NULL* [] | LUN ID   |
| description       | text *NULL*            | 描述     |
| raid_level        | varchar(255) *NULL* [] | 阵列级别 |
| size              | varchar(255) *NULL* [] | 容量     |
| storagesystem_id  | int *NULL* [**0**]     | 存储系统 |
| obsolescence_date | date *NULL*            | 废弃时间 |

### 索引

| PRIMARY | *id*               |
| :------ | ------------------ |
| INDEX   | *name*(95)         |
| INDEX   | *storagesystem_id* |