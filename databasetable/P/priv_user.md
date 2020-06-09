| 列         | 类型                                            | 注释 |
| :--------- | ----------------------------------------------- | ---- |
| id         | int *自动增量*                                  |      |
| contactid  | int *NULL* [**0**]                              |      |
| login      | varchar(255) *NULL* []                          |      |
| language   | varchar(255) *NULL* [**EN US**]                 |      |
| status     | enum('disabled','enabled') *NULL* [**enabled**] |      |
| finalclass | varchar(255) *NULL* [**User**]                  |      |

### 索引

| PRIMARY | *id*             |
| :------ | ---------------- |
| INDEX   | *contactid*      |
| INDEX   | *login*(95)      |
| INDEX   | *language*(95)   |
| INDEX   | *finalclass*(95) |