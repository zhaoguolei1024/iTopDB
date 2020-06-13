person

个人 (Person)

联系人 (Contact) >> Person



| 列               | 类型                   | 注释     |
| :--------------- | ---------------------- | -------- |
| id               | int *自动增量*         | 自增ID   |
| picture_data     | longblob *NULL*        |          |
| picture_mimetype | varchar(255) *NULL*    |          |
| picture_filename | varchar(255) *NULL*    |          |
| first_name       | varchar(255) *NULL* [] | 姓名     |
| employee_number  | varchar(255) *NULL* [] | 员工编号 |
| mobile_phone     | varchar(255) *NULL* [] | 移动电话 |
| location_id      | int *NULL* [**0**]     | 地理位置 |
| manager_id       | int *NULL* [**0**]     | 经理     |

### 索引

| PRIMARY | *id*             |
| :------ | ---------------- |
| INDEX   | *first_name*(95) |
| INDEX   | *location_id*    |
| INDEX   | *manager_id*     |