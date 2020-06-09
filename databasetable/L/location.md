| 列                | 类型                                          | 注释 |
| :---------------- | --------------------------------------------- | ---- |
| id                | int *自动增量*                                |      |
| name              | varchar(255) *NULL* []                        |      |
| status            | enum('active','inactive') *NULL* [**active**] |      |
| org_id            | int *NULL* [**0**]                            |      |
| address           | text *NULL*                                   |      |
| postal_code       | varchar(255) *NULL* []                        |      |
| city              | varchar(255) *NULL* []                        |      |
| country           | varchar(255) *NULL* []                        |      |
| obsolescence_date | date *NULL*                                   |      |

### 索引

| PRIMARY | *id*       |
| :------ | ---------- |
| INDEX   | *name*(95) |
| INDEX   | *org_id*   |