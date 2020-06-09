| 列            | 类型                   | 注释 |
| :------------ | ---------------------- | ---- |
| id            | int *自动增量*         |      |
| name          | varchar(255) *NULL* [] |      |
| icon_data     | longblob *NULL*        |      |
| icon_mimetype | varchar(255) *NULL*    |      |
| icon_filename | varchar(255) *NULL*    |      |

### 索引

| PRIMARY | *id*       |
| :------ | ---------- |
| INDEX   | *name*(95) |