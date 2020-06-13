priv_trigger

触发器 (Trigger) - Custom event handler



| 列          | 类型                              | 注释   |
| :---------- | --------------------------------- | ------ |
| id          | int *自动增量*                    | 自增ID |
| description | varchar(255) *NULL* []            | 描述   |
| context     | varchar(255) *NULL* []            | 内容   |
| realclass   | varchar(255) *NULL* [**Trigger**] | 分类   |

### 索引

| PRIMARY | *id*              |
| :------ | ----------------- |
| INDEX   | *description*(95) |
| INDEX   | *realclass*(95)   |