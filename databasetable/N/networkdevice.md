| 列                   | 类型                   | 注释 |
| :------------------- | ---------------------- | ---- |
| id                   | int *自动增量*         |      |
| networkdevicetype_id | int *NULL* [**0**]     |      |
| iosversion_id        | int *NULL* [**0**]     |      |
| ram                  | varchar(255) *NULL* [] |      |

### 索引

| PRIMARY | *id*                   |
| :------ | ---------------------- |
| INDEX   | *networkdevicetype_id* |
| INDEX   | *iosversion_id*        |