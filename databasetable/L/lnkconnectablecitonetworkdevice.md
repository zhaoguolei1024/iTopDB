lnkconnectablecitonetworkdevice



链接 可连接项 / 网络设备 (lnkConnectableCIToNetworkDevice)



| 列               | 类型                                            | 注释                                     |
| :--------------- | ----------------------------------------------- | ---------------------------------------- |
| id               | int *自动增量*                                  | 自增ID                                   |
| networkdevice_id | int *NULL* [**0**]                              | 网络设备                                 |
| connectableci_id | int *NULL* [**0**]                              | 可连接的设备                             |
| network_port     | varchar(255) *NULL* []                          | 网络端口                                 |
| device_port      | varchar(255) *NULL* []                          | 设备端口                                 |
| type             | enum('downlink','uplink') *NULL* [**downlink**] | 连接类型，下联 (downlink), 上联 (uplink) |

### 索引

| PRIMARY | *id*               |
| :------ | ------------------ |
| INDEX   | *networkdevice_id* |
| INDEX   | *connectableci_id* |



注：连接类型 (connection_type)与字段type不一致