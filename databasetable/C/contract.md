contract

合同



| 列                | 类型                                                  | 注释                                                         |
| :---------------- | ----------------------------------------------------- | ------------------------------------------------------------ |
| id                | int *自动增量*                                        | 自增ID                                                       |
| name              | varchar(255) *NULL* []                                | 名称                                                         |
| org_id            | int *NULL* [**0**]                                    | 客户，组织 (Organization)的外键                              |
| description       | text *NULL*                                           | 描述                                                         |
| start_date        | date *NULL*                                           | 开始日期                                                     |
| end_date          | date *NULL*                                           | 结束日期                                                     |
| cost              | varchar(255) *NULL* []                                | 计费                                                         |
| cost_currency     | enum('dollars','euros') *NULL*                        | 结算货币，美元 (dollars), 欧元 (euros)                       |
| contracttype_id   | int *NULL* [**0**]                                    | 合同类型                                                     |
| billing_frequency | varchar(255) *NULL* []                                | 付款周期                                                     |
| cost_unit         | varchar(255) *NULL* []                                | 计费单位                                                     |
| provider_id       | int *NULL* [**0**]                                    | 供应商，组织 (Organization)的外键                            |
| status            | enum('implementation','obsolete','production') *NULL* | 状态，启用 (implementation), 废弃 (obsolete), 生产 (production) |
| finalclass        | varchar(255) *NULL* [**Contract**]                    | 类型                                                         |

### 索引

| PRIMARY | *id*              |
| :------ | ----------------- |
| INDEX   | *name*(95)        |
| INDEX   | *org_id*          |
| INDEX   | *contracttype_id* |
| INDEX   | *provider_id*     |
| INDEX   | *finalclass*(95)  |