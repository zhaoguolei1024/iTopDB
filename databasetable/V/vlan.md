vlan

VLAN (VLAN)



| 列          | 类型                   | 注释      |
| :---------- | ---------------------- | --------- |
| id          | int *自动增量*         | 自增ID    |
| vlan_tag    | varchar(255) *NULL* [] | VLAN 标记 |
| description | text *NULL*            | 描述      |
| org_id      | int *NULL* [**0**]     | 组织ID    |

### 索引

| PRIMARY | *id*           |
| :------ | -------------- |
| INDEX   | *vlan_tag*(95) |
| INDEX   | *org_id*       |