knownerror

已知错误 (KnownError) - 记录一个已知错误





| 列         | 类型                                                         | 注释                                                         |
| :--------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| id         | int *自动增量*                                               | 自增ID                                                       |
| name       | varchar(255) *NULL* []                                       | 名称                                                         |
| cust_id    | int *NULL* [**0**]                                           |                                                              |
| problem_id | int *NULL* [**0**]                                           | 相关问题                                                     |
| symptom    | text *NULL*                                                  | 现象                                                         |
| rootcause  | text *NULL*                                                  | 问题根源                                                     |
| workaround | text *NULL*                                                  | 解决过程                                                     |
| solution   | text *NULL*                                                  | 解决方案                                                     |
| error_code | varchar(255) *NULL* []                                       | 错误代码                                                     |
| domain     | enum('Application','Desktop','Network','Server') *NULL* [**Application**] | 类型，应用 (Application), 桌面 (Desktop), 网络 (Network), 服务器 (Server) |
| vendor     | varchar(255) *NULL* []                                       | 厂商                                                         |
| model      | varchar(255) *NULL* []                                       | 型号                                                         |
| version    | varchar(255) *NULL* []                                       | 版本                                                         |

### 索引

| PRIMARY | *id*         |
| :------ | ------------ |
| INDEX   | *name*(95)   |
| INDEX   | *cust_id*    |
| INDEX   | *problem_id* |