| 列                | 类型                                                  | 注释 |
| :---------------- | ----------------------------------------------------- | ---- |
| id                | int *自动增量*                                        |      |
| name              | varchar(255) *NULL* []                                |      |
| org_id            | int *NULL* [**0**]                                    |      |
| description       | text *NULL*                                           |      |
| start_date        | date *NULL*                                           |      |
| end_date          | date *NULL*                                           |      |
| cost              | varchar(255) *NULL* []                                |      |
| cost_currency     | enum('dollars','euros') *NULL*                        |      |
| contracttype_id   | int *NULL* [**0**]                                    |      |
| billing_frequency | varchar(255) *NULL* []                                |      |
| cost_unit         | varchar(255) *NULL* []                                |      |
| provider_id       | int *NULL* [**0**]                                    |      |
| status            | enum('implementation','obsolete','production') *NULL* |      |
| finalclass        | varchar(255) *NULL* [**Contract**]                    |      |

### 索引

| PRIMARY | *id*              |
| :------ | ----------------- |
| INDEX   | *name*(95)        |
| INDEX   | *org_id*          |
| INDEX   | *contracttype_id* |
| INDEX   | *provider_id*     |
| INDEX   | *finalclass*(95)  |