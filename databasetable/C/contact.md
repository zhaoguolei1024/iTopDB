contact

联系人

| 列                | 类型                                          | 注释                                 |
| :---------------- | --------------------------------------------- | ------------------------------------ |
| id                | int *自动增量*                                | 自增ID                               |
| name              | varchar(255) *NULL* []                        | 名称                                 |
| status            | enum('active','inactive') *NULL* [**active**] | 状态；启用 (active), 停用 (inactive) |
| org_id            | int *NULL* [**0**]                            | 组织ID，组织 (Organization)的外键    |
| email             | varchar(255) *NULL* []                        | 邮箱地址                             |
| phone             | varchar(255) *NULL* []                        | 电话号码                             |
| notify            | enum('no','yes') *NULL* [**yes**]             | 通知；否 (no), 是 (yes)              |
| function          | varchar(255) *NULL* []                        | 职责                                 |
| finalclass        | varchar(255) *NULL* [**Contact**]             | 联系人子类别                         |
| obsolescence_date | date *NULL*                                   | 废弃时间                             |

### 索引

| PRIMARY | *id*             |
| :------ | ---------------- |
| INDEX   | *name*(95)       |
| INDEX   | *org_id*         |
| INDEX   | *finalclass*(95) |