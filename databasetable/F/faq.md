faq

问题解答

| 列          | 类型                   | 注释     |
| :---------- | ---------------------- | -------- |
| id          | int *自动增量*         | 自增ID   |
| title       | varchar(255) *NULL* [] | 标题     |
| summary     | text *NULL*            | 概要     |
| description | longtext *NULL*        | 描述     |
| category_id | int *NULL* [**0**]     | 类别     |
| error_code  | varchar(255) *NULL* [] | 错误代码 |
| key_words   | varchar(255) *NULL* [] | 关键字   |
| domains     | varchar(255) *NULL* [] | Domains  |

### 索引

| PRIMARY | *id*          |
| :------ | ------------- |
| INDEX   | *title*(95)   |
| INDEX   | *category_id* |

