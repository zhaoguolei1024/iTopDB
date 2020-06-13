servicefamily

服务族 (ServiceFamily)



| 列            | 类型                   | 注释     |
| :------------ | ---------------------- | -------- |
| id            | int *自动增量*         | 自增ID   |
| name          | varchar(255) *NULL* [] | 名称     |
| icon_data     | longblob *NULL*        | 图标数据 |
| icon_mimetype | varchar(255) *NULL*    | 图标类型 |
| icon_filename | varchar(255) *NULL*    | 图标文件 |

### 索引

| PRIMARY | *id*       |
| :------ | ---------- |
| INDEX   | *name*(95) |