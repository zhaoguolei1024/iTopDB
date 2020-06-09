| 列          | 类型                   | 注释 |
| :---------- | ---------------------- | ---- |
| id          | int *自动增量*         |      |
| userid      | int *NULL* [**0**]     |      |
| profileid   | int *NULL* [**0**]     |      |
| description | varchar(255) *NULL* [] |      |

### 索引

| PRIMARY | *id*        |
| :------ | ----------- |
| INDEX   | *userid*    |
| INDEX   | *profileid* |