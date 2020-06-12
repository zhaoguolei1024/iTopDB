connectableci

可连接的配置项

| 列         | 类型                                    | 注释       |
| :--------- | --------------------------------------- | ---------- |
| id         | int *自动增量*                          | 自增ID     |
| finalclass | varchar(255) *NULL* [**ConnectableCI**] | 二级配置项 |

### 索引

| PRIMARY | *id*             |
| :------ | ---------------- |
| INDEX   | *finalclass*(95) |