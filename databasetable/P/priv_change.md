priv_change







| 列       | 类型                                                         | 注释     |
| :------- | ------------------------------------------------------------ | -------- |
| id       | int *自动增量*                                               | 自增ID   |
| date     | datetime *NULL*                                              | 时间     |
| userinfo | varchar(255) *NULL* []                                       | 用户信息 |
| origin   | enum('csv-import.php','csv-interactive','custom-extension','email-processing','interactive','synchro-data-source','webservice-rest','webservice-soap') *NULL* [**interactive**] | 来源     |

### 索引

| PRIMARY | *id*     |
| :------ | -------- |
| INDEX   | *date*   |
| INDEX   | *origin* |