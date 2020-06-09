| 列          | 类型                   | 注释 |
| :---------- | ---------------------- | ---- |
| id          | int *自动增量*         |      |
| vlan_tag    | varchar(255) *NULL* [] |      |
| description | text *NULL*            |      |
| org_id      | int *NULL* [**0**]     |      |

### 索引

| PRIMARY | *id*           |
| :------ | -------------- |
| INDEX   | *vlan_tag*(95) |
| INDEX   | *org_id*       |