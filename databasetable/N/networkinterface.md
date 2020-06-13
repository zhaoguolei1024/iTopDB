networkinterface

网卡 (NetworkInterface)





| 列                | 类型                                       | 注释       |
| :---------------- | ------------------------------------------ | ---------- |
| id                | int *自动增量*                             | 自增ID     |
| name              | varchar(255) *NULL* []                     | 名称       |
| finalclass        | varchar(255) *NULL* [**NetworkInterface**] | 网卡子类别 |
| obsolescence_date | date *NULL*                                | 废弃时间   |

### 索引

| PRIMARY | *id*             |
| :------ | ---------------- |
| INDEX   | *name*(95)       |
| INDEX   | *finalclass*(95) |