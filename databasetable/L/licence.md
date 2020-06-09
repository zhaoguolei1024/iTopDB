| 列                | 类型                              | 注释 |
| :---------------- | --------------------------------- | ---- |
| id                | int *自动增量*                    |      |
| name              | varchar(255) *NULL* []            |      |
| org_id            | int *NULL* [**0**]                |      |
| usage_limit       | varchar(255) *NULL* []            |      |
| description       | text *NULL*                       |      |
| start_date        | date *NULL*                       |      |
| end_date          | date *NULL*                       |      |
| licence_key       | varchar(255) *NULL* []            |      |
| perpetual         | enum('no','yes') *NULL* [**no**]  |      |
| finalclass        | varchar(255) *NULL* [**Licence**] |      |
| obsolescence_date | date *NULL*                       |      |

### 索引

| PRIMARY | *id*             |
| :------ | ---------------- |
| INDEX   | *name*(95)       |
| INDEX   | *org_id*         |
| INDEX   | *finalclass*(95) |