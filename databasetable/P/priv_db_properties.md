priv_db_properties

DB 属性 (DBProperty)



| 列             | 类型                   | 注释     |
| :------------- | ---------------------- | -------- |
| id             | int *自动增量*         | ID       |
| name           | varchar(255) *NULL* [] | 名称     |
| description    | varchar(255) *NULL* [] | 描述     |
| value          | varchar(255) *NULL* [] | 值       |
| change_date    | datetime *NULL*        | 修改日期 |
| change_comment | varchar(255) *NULL* [] | 备注     |

### 索引

| PRIMARY | *id*       |
| :------ | ---------- |
| INDEX   | *name*(95) |