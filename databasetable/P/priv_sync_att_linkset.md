priv_sync_att_linkset

Synchro Attribute (Linkset) (SynchroAttLinkSet)



| 列                  | 类型                         | 注释         |
| :------------------ | ---------------------------- | ------------ |
| id                  | int *自动增量*               | 自增ID       |
| row_separator       | varchar(255) *NULL* [**\|**] | 列的分隔符   |
| attribute_separator | varchar(255) *NULL* [**;**]  | 属性的分隔符 |
| value_separator     | varchar(255) *NULL* [**:**]  | 值的分隔符   |
| attribute_qualifier | varchar(255) *NULL* [**'**]  | 属性的限定符 |

### 索引

| PRIMARY | *id* |
| :------ | ---- |
|         |      |