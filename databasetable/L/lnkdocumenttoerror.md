| 列          | 类型                   | 注释 |
| :---------- | ---------------------- | ---- |
| link_id     | int *自动增量*         |      |
| document_id | int *NULL* [**0**]     |      |
| error_id    | int *NULL* [**0**]     |      |
| link_type   | varchar(255) *NULL* [] |      |

### 索引

| PRIMARY | *link_id*       |
| :------ | --------------- |
| INDEX   | *document_id*   |
| INDEX   | *error_id*      |
| INDEX   | *link_type*(95) |