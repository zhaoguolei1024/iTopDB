| 列       | 类型                                                         | 注释 |
| :------- | ------------------------------------------------------------ | ---- |
| id       | int *自动增量*                                               |      |
| date     | datetime *NULL*                                              |      |
| userinfo | varchar(255) *NULL* []                                       |      |
| origin   | enum('csv-import.php','csv-interactive','custom-extension','email-processing','interactive','synchro-data-source','webservice-rest','webservice-soap') *NULL* [**interactive**] |      |

### 索引

| PRIMARY | *id*     |
| :------ | -------- |
| INDEX   | *date*   |
| INDEX   | *origin* |