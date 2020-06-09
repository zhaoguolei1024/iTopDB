| 列                | 类型                                                         | 注释 |
| :---------------- | ------------------------------------------------------------ | ---- |
| id                | int *自动增量*                                               |      |
| status            | enum('error','idle','planned','running') *NULL* [**planned**] |      |
| created           | datetime *NULL*                                              |      |
| started           | datetime *NULL*                                              |      |
| planned           | datetime *NULL*                                              |      |
| event_id          | int *NULL* [**0**]                                           |      |
| remaining_retries | int *NULL* [**0**]                                           |      |
| last_error_code   | int *NULL* [**0**]                                           |      |
| last_error        | varchar(255) *NULL* []                                       |      |
| last_attempt      | datetime *NULL*                                              |      |
| realclass         | varchar(255) *NULL* [**AsyncTask**]                          |      |

### 索引

| PRIMARY | *id*            |
| :------ | --------------- |
| INDEX   | *created*       |
| INDEX   | *event_id*      |
| INDEX   | *realclass*(95) |