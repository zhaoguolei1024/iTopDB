nasfilesystem

NAS 文件系统 (NASFileSystem)





| 列                | 类型                   | 注释     |
| :---------------- | ---------------------- | -------- |
| id                | int *自动增量*         | 自增ID   |
| name              | varchar(255) *NULL* [] | 名称     |
| description       | text *NULL*            | 描述     |
| raid_level        | varchar(255) *NULL* [] | 阵列级别 |
| size              | varchar(255) *NULL* [] | 容量     |
| nas_id            | int *NULL* [**0**]     | NAS      |
| obsolescence_date | date *NULL*            | 废弃时间 |

### 索引

| PRIMARY | *id*       |
| :------ | ---------- |
| INDEX   | *name*(95) |
| INDEX   | *nas_id*   |