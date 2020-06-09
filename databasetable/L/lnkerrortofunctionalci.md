| 列              | 类型                   | 注释 |
| :-------------- | ---------------------- | ---- |
| link_id         | int *自动增量*         |      |
| functionalci_id | int *NULL* [**0**]     |      |
| error_id        | int *NULL* [**0**]     |      |
| dummy           | varchar(255) *NULL* [] |      |

### 索引

| PRIMARY | *link_id*         |
| :------ | ----------------- |
| INDEX   | *functionalci_id* |
| INDEX   | *error_id*        |