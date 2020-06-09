| 列          | 类型                   | 注释 |
| :---------- | ---------------------- | ---- |
| id          | int *自动增量*         |      |
| title       | varchar(255) *NULL* [] |      |
| summary     | text *NULL*            |      |
| description | longtext *NULL*        |      |
| category_id | int *NULL* [**0**]     |      |
| error_code  | varchar(255) *NULL* [] |      |
| key_words   | varchar(255) *NULL* [] |      |
| domains     | varchar(255) *NULL* [] |      |

### 索引

| PRIMARY | *id*          |
| :------ | ------------- |
| INDEX   | *title*(95)   |
| INDEX   | *category_id* |