functionalci



功能配置项 (FunctionalCI)



| 列                 | 类型                                         | 注释                                         |
| :----------------- | -------------------------------------------- | -------------------------------------------- |
| id                 | int *自动增量*                               | 自增ID                                       |
| name               | varchar(255) *NULL* []                       | 名称                                         |
| description        | text *NULL*                                  | 描述                                         |
| org_id             | int *NULL* [**0**]                           | 组织                                         |
| business_criticity | enum('high','low','medium') *NULL* [**low**] | 业务重要性，高 (high), 低 (low), 中 (medium) |
| move2production    | date *NULL*                                  | 投产日期                                     |
| finalclass         | varchar(255) *NULL* [**FunctionalCI**]       | 二级配置项                                   |
| obsolescence_date  | date *NULL*                                  | 废弃时间                                     |

### 索引

| PRIMARY | *id*             |
| :------ | ---------------- |
| INDEX   | *name*(95)       |
| INDEX   | *org_id*         |
| INDEX   | *finalclass*(95) |