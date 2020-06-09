| 列                | 类型                                          | 注释 |
| :---------------- | --------------------------------------------- | ---- |
| id                | int *自动增量*                                |      |
| name              | varchar(255) *NULL* []                        |      |
| status            | enum('active','inactive') *NULL* [**active**] |      |
| org_id            | int *NULL* [**0**]                            |      |
| email             | varchar(255) *NULL* []                        |      |
| phone             | varchar(255) *NULL* []                        |      |
| notify            | enum('no','yes') *NULL* [**yes**]             |      |
| function          | varchar(255) *NULL* []                        |      |
| finalclass        | varchar(255) *NULL* [**Contact**]             |      |
| obsolescence_date | date *NULL*                                   |      |

### 索引

| PRIMARY | *id*             |
| :------ | ---------------- |
| INDEX   | *name*(95)       |
| INDEX   | *org_id*         |
| INDEX   | *finalclass*(95) |