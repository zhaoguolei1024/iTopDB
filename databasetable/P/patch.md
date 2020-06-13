patch

补丁 (Patch)



| 列          | 类型                            | 注释       |
| :---------- | ------------------------------- | ---------- |
| id          | int *自动增量*                  | 自增ID     |
| name        | varchar(255) *NULL* []          | 名称       |
| description | text *NULL*                     | 描述       |
| finalclass  | varchar(255) *NULL* [**Patch**] | 补丁子类别 |

### 索引

| PRIMARY | *id*             |
| :------ | ---------------- |
| INDEX   | *name*(95)       |
| INDEX   | *finalclass*(95) |