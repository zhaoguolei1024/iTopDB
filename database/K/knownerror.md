| 列         | 类型                                                         | 注释 |
| :--------- | ------------------------------------------------------------ | ---- |
| id         | int *自动增量*                                               |      |
| name       | varchar(255) *NULL* []                                       |      |
| cust_id    | int *NULL* [**0**]                                           |      |
| problem_id | int *NULL* [**0**]                                           |      |
| symptom    | text *NULL*                                                  |      |
| rootcause  | text *NULL*                                                  |      |
| workaround | text *NULL*                                                  |      |
| solution   | text *NULL*                                                  |      |
| error_code | varchar(255) *NULL* []                                       |      |
| domain     | enum('Application','Desktop','Network','Server') *NULL* [**Application**] |      |
| vendor     | varchar(255) *NULL* []                                       |      |
| model      | varchar(255) *NULL* []                                       |      |
| version    | varchar(255) *NULL* []                                       |      |

### 索引

| PRIMARY | *id*         |
| :------ | ------------ |
| INDEX   | *name*(95)   |
| INDEX   | *cust_id*    |
| INDEX   | *problem_id* |