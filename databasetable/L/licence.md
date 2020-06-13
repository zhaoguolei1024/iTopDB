licence

许可证 (Licence)





| 列                | 类型                              | 注释                        |
| :---------------- | --------------------------------- | --------------------------- |
| id                | int *自动增量*                    | 自增ID                      |
| name              | varchar(255) *NULL* []            | 名称                        |
| org_id            | int *NULL* [**0**]                | 组织                        |
| usage_limit       | varchar(255) *NULL* []            | 使用限制                    |
| description       | text *NULL*                       | 描述                        |
| start_date        | date *NULL*                       | 开始日期                    |
| end_date          | date *NULL*                       | 结束日期                    |
| licence_key       | varchar(255) *NULL* []            | 密钥                        |
| perpetual         | enum('no','yes') *NULL* [**no**]  | 永久有效，否 (no), 是 (yes) |
| finalclass        | varchar(255) *NULL* [**Licence**] | 许可证子类别                |
| obsolescence_date | date *NULL*                       | 废弃时间                    |

### 索引

| PRIMARY | *id*             |
| :------ | ---------------- |
| INDEX   | *name*(95)       |
| INDEX   | *org_id*         |
| INDEX   | *finalclass*(95) |