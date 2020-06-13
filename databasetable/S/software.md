software

软件 (Software)



| 列      | 类型                                                         | 注释                                                         |
| :------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| id      | int *自动增量*                                               | 自增ID                                                       |
| name    | varchar(255) *NULL* []                                       | 名称                                                         |
| vendor  | varchar(255) *NULL* []                                       | 厂商                                                         |
| version | varchar(255) *NULL* []                                       | 版本                                                         |
| type    | enum('DBServer','Middleware','OtherSoftware','PCSoftware','WebServer') *NULL* | 类型，数据库服务器 (DBServer), 中间件 (Middleware), 其它软件 (OtherSoftware), PC 软件 (PCSoftware), Web 服务器 (WebServer) |

### 索引

| PRIMARY | *id*          |
| :------ | ------------- |
| INDEX   | *name*(95)    |
| INDEX   | *version*(95) |