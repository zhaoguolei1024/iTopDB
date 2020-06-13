typology

拓扑 (Typology)



| 列         | 类型                               | 注释       |
| :--------- | ---------------------------------- | ---------- |
| id         | int *自动增量*                     | 自增ID     |
| name       | varchar(255) *NULL* []             | 名称       |
| finalclass | varchar(255) *NULL* [**Typology**] | 拓扑子类别 |

### 索引

| PRIMARY | *id*             |
| :------ | ---------------- |
| INDEX   | *name*(95)       |
| INDEX   | *finalclass*(95) |