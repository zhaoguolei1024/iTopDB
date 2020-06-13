priv_tagfielddata

Tag Set Field Data (TagSetFieldData)



| 列          | 类型                                      | 注释         |
| :---------- | ----------------------------------------- | ------------ |
| id          | int *自动增量*                            | 自增ID       |
| code        | varchar(255) *NULL* []                    | 代码         |
| label       | varchar(255) *NULL* []                    | 标签         |
| description | longtext *NULL*                           | 描述         |
| obj_class   | varchar(255) *NULL* []                    | 对象分类     |
| obj_attcode | varchar(255) *NULL* []                    | 对象熟悉代码 |
| finalclass  | varchar(255) *NULL* [**TagSetFieldData**] | tag分类      |

### 索引

| PRIMARY | *id*             |
| :------ | ---------------- |
| INDEX   | *label*(95)      |
| INDEX   | *finalclass*(95) |