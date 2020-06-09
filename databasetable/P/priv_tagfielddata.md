| 列          | 类型                                      | 注释 |
| :---------- | ----------------------------------------- | ---- |
| id          | int *自动增量*                            |      |
| code        | varchar(255) *NULL* []                    |      |
| label       | varchar(255) *NULL* []                    |      |
| description | longtext *NULL*                           |      |
| obj_class   | varchar(255) *NULL* []                    |      |
| obj_attcode | varchar(255) *NULL* []                    |      |
| finalclass  | varchar(255) *NULL* [**TagSetFieldData**] |      |

### 索引

| PRIMARY | *id*             |
| :------ | ---------------- |
| INDEX   | *label*(95)      |
| INDEX   | *finalclass*(95) |