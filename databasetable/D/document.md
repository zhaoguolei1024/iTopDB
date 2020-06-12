| 列                | 类型                                        | 注释 |
| :---------------- | ------------------------------------------- | ---- |
| id                | int *自动增量*                              |      |
| name              | varchar(255) *NULL* []                      |      |
| org_id            | int *NULL* [**0**]                          |      |
| documenttype_id   | int *NULL* [**0**]                          |      |
| version           | varchar(255) *NULL* []                      |      |
| description       | text *NULL*                                 |      |
| status            | enum('draft','obsolete','published') *NULL* |      |
| finalclass        | varchar(255) *NULL* [**Document**]          |      |
| obsolescence_date | date *NULL*                                 |      |

### 索引

| PRIMARY | *id*              |
| :------ | ----------------- |
| INDEX   | *org_id*          |
| INDEX   | *documenttype_id* |
| INDEX   | *finalclass*(95)  |