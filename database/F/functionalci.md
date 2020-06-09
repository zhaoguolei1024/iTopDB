| 列                 | 类型                                         | 注释 |
| :----------------- | -------------------------------------------- | ---- |
| id                 | int *自动增量*                               |      |
| name               | varchar(255) *NULL* []                       |      |
| description        | text *NULL*                                  |      |
| org_id             | int *NULL* [**0**]                           |      |
| business_criticity | enum('high','low','medium') *NULL* [**low**] |      |
| move2production    | date *NULL*                                  |      |
| finalclass         | varchar(255) *NULL* [**FunctionalCI**]       |      |
| obsolescence_date  | date *NULL*                                  |      |

### 索引

| PRIMARY | *id*             |
| :------ | ---------------- |
| INDEX   | *name*(95)       |
| INDEX   | *org_id*         |
| INDEX   | *finalclass*(95) |