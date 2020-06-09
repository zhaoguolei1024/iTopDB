## attachment

## 附件

| 列                | 类型                   | 注释 |
| :---------------- | ---------------------- | ---- |
| id                | int *自动增量*         |      |
| expire            | datetime *NULL*        |      |
| temp_id           | varchar(255) *NULL* [] |      |
| item_class        | varchar(255) *NULL* [] |      |
| item_id           | int *NULL* [**0**]     |      |
| item_org_id       | int *NULL* [**0**]     |      |
| contents_data     | longblob *NULL*        |      |
| contents_mimetype | varchar(255) *NULL*    |      |
| contents_filename | varchar(255) *NULL*    |      |
| creation_date     | datetime *NULL*        |      |
| user_id           | int *NULL* [**0**]     |      |

### 索引

| PRIMARY | *id*                        |
| :------ | --------------------------- |
| INDEX   | *temp_id*(95)               |
| INDEX   | *item_class*(95)            |
| INDEX   | *user_id*                   |
| INDEX   | *item_class*(95), *item_id* |
| INDEX   | *item_org_id*               |