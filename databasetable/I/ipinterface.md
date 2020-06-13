

ipinterface

网卡 (NetworkInterface) >> IPInterface

IP Interface (IPInterface)



| 列         | 类型                                  | 注释       |
| :--------- | ------------------------------------- | ---------- |
| id         | int *自动增量*                        | 自增ID     |
| ipaddress  | varchar(255) *NULL* []                | IP 地址    |
| macaddress | varchar(255) *NULL* []                | MAC 地址   |
| comment    | text *NULL*                           | 注释       |
| ipgateway  | varchar(255) *NULL* []                | 网关       |
| ipmask     | varchar(255) *NULL* []                | 掩码       |
| speed      | decimal(12,2) *NULL*                  | 速率       |
| finalclass | varchar(255) *NULL* [**IPInterface**] | 网卡子类别 |

### 索引

| PRIMARY | *id*             |
| :------ | ---------------- |
| INDEX   | *finalclass*(95) |