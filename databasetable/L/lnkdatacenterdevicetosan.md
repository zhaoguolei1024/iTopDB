| 列                    | 类型                   | 注释 |
| :-------------------- | ---------------------- | ---- |
| id                    | int *自动增量*         |      |
| san_id                | int *NULL* [**0**]     |      |
| datacenterdevice_id   | int *NULL* [**0**]     |      |
| san_port              | varchar(255) *NULL* [] |      |
| datacenterdevice_port | varchar(255) *NULL* [] |      |

### 索引

| PRIMARY | *id*                  |
| :------ | --------------------- |
| INDEX   | *san_id*              |
| INDEX   | *datacenterdevice_id* |