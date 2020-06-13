priv_query

查询 (Query) - 查询是一种动态的数据集

抽象类: 该类不能实例化对象.



| 列          | 类型                            | 注释   |
| :---------- | ------------------------------- | ------ |
| id          | int *自动增量*                  | 自增ID |
| name        | varchar(255) *NULL* []          | 名称   |
| description | text *NULL*                     | 描述   |
| realclass   | varchar(255) *NULL* [**Query**] | 分类   |

### 索引

| PRIMARY | *id*            |
| :------ | --------------- |
| INDEX   | *name*(95)      |
| INDEX   | *realclass*(95) |