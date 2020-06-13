tape

磁带 (Tape)



| 列                | 类型                   | 注释     |
| :---------------- | ---------------------- | -------- |
| id                | int *自动增量*         | 自增ID   |
| name              | varchar(255) *NULL* [] | 名称     |
| description       | text *NULL*            | 描述     |
| size              | varchar(255) *NULL* [] | 容量     |
| tapelibrary_id    | int *NULL* [**0**]     | 磁带库ID |
| obsolescence_date | date *NULL*            | 废弃时间 |

### 索引

| PRIMARY | *id*             |
| :------ | ---------------- |
| INDEX   | *name*(95)       |
| INDEX   | *tapelibrary_id* |