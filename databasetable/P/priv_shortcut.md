priv_shortcut

快捷方式 (Shortcut)

抽象类: 该类不能实例化对象.

| 列        | 类型                               | 注释   |
| :-------- | ---------------------------------- | ------ |
| id        | int *自动增量*                     | 自增ID |
| user_id   | int *NULL* [**0**]                 | 账户   |
| name      | varchar(255) *NULL* []             | 名称   |
| context   | text *NULL*                        | 内容   |
| realclass | varchar(255) *NULL* [**Shortcut**] | 类别   |

### 索引

| PRIMARY | *id*            |
| :------ | --------------- |
| INDEX   | *user_id*       |
| INDEX   | *name*(95)      |
| INDEX   | *realclass*(95) |