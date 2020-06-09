| 列               | 类型                   | 注释 |
| :--------------- | ---------------------- | ---- |
| id               | int *自动增量*         |      |
| picture_data     | longblob *NULL*        |      |
| picture_mimetype | varchar(255) *NULL*    |      |
| picture_filename | varchar(255) *NULL*    |      |
| first_name       | varchar(255) *NULL* [] |      |
| employee_number  | varchar(255) *NULL* [] |      |
| mobile_phone     | varchar(255) *NULL* [] |      |
| location_id      | int *NULL* [**0**]     |      |
| manager_id       | int *NULL* [**0**]     |      |

### 索引

| PRIMARY | *id*             |
| :------ | ---------------- |
| INDEX   | *first_name*(95) |
| INDEX   | *location_id*    |
| INDEX   | *manager_id*     |