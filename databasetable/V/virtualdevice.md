| 列         | 类型                                                         | 注释 |
| :--------- | ------------------------------------------------------------ | ---- |
| id         | int *自动增量*                                               |      |
| status     | enum('implementation','obsolete','production','stock') *NULL* [**production**] |      |
| finalclass | varchar(255) *NULL* [**VirtualDevice**]                      |      |

### 索引

| PRIMARY | *id*             |
| :------ | ---------------- |
| INDEX   | *finalclass*(95) |