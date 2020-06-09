| 列                  | 类型                   | 注释 |
| :------------------ | ---------------------- | ---- |
| id                  | int *自动增量*         |      |
| speed               | decimal(6,2) *NULL*    |      |
| topology            | varchar(255) *NULL* [] |      |
| wwn                 | varchar(255) *NULL* [] |      |
| datacenterdevice_id | int *NULL* [**0**]     |      |

### 索引

| PRIMARY | *id*                  |
| :------ | --------------------- |
| INDEX   | *datacenterdevice_id* |