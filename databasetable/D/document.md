document

文档



| 列                | 类型                                        | 注释                                                    |
| :---------------- | ------------------------------------------- | ------------------------------------------------------- |
| id                | int *自动增量*                              | 自增ID                                                  |
| name              | varchar(255) *NULL* []                      | 名称                                                    |
| org_id            | int *NULL* [**0**]                          | 组织                                                    |
| documenttype_id   | int *NULL* [**0**]                          | 文档类型                                                |
| version           | varchar(255) *NULL* []                      | 版本                                                    |
| description       | text *NULL*                                 | 描述                                                    |
| status            | enum('draft','obsolete','published') *NULL* | 状态，草稿 (draft), 废弃 (obsolete), 已发布 (published) |
| finalclass        | varchar(255) *NULL* [**Document**]          | 文档子类别                                              |
| obsolescence_date | date *NULL*                                 | 废弃时间                                                |

### 索引

| PRIMARY | *id*              |
| :------ | ----------------- |
| INDEX   | *org_id*          |
| INDEX   | *documenttype_id* |
| INDEX   | *finalclass*(95)  |