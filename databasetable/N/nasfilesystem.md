| 列                | 类型                   | 注释 |
| :---------------- | ---------------------- | ---- |
| id                | int *自动增量*         |      |
| name              | varchar(255) *NULL* [] |      |
| description       | text *NULL*            |      |
| raid_level        | varchar(255) *NULL* [] |      |
| size              | varchar(255) *NULL* [] |      |
| nas_id            | int *NULL* [**0**]     |      |
| obsolescence_date | date *NULL*            |      |

### 索引

| PRIMARY | *id*       |
| :------ | ---------- |
| INDEX   | *name*(95) |
| INDEX   | *nas_id*   |