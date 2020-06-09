| 列               | 类型                                                  | 注释 |
| :--------------- | ----------------------------------------------------- | ---- |
| id               | int *自动增量*                                        |      |
| name             | varchar(255) *NULL* []                                |      |
| org_id           | int *NULL* [**0**]                                    |      |
| servicefamily_id | int *NULL* [**0**]                                    |      |
| description      | text *NULL*                                           |      |
| status           | enum('implementation','obsolete','production') *NULL* |      |
| icon_data        | longblob *NULL*                                       |      |
| icon_mimetype    | varchar(255) *NULL*                                   |      |
| icon_filename    | varchar(255) *NULL*                                   |      |

### 索引

| PRIMARY | *id*               |
| :------ | ------------------ |
| INDEX   | *name*(95)         |
| INDEX   | *org_id*           |
| INDEX   | *servicefamily_id* |