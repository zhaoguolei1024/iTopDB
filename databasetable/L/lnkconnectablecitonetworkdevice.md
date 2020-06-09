| 列               | 类型                                            | 注释 |
| :--------------- | ----------------------------------------------- | ---- |
| id               | int *自动增量*                                  |      |
| networkdevice_id | int *NULL* [**0**]                              |      |
| connectableci_id | int *NULL* [**0**]                              |      |
| network_port     | varchar(255) *NULL* []                          |      |
| device_port      | varchar(255) *NULL* []                          |      |
| type             | enum('downlink','uplink') *NULL* [**downlink**] |      |

### 索引

| PRIMARY | *id*               |
| :------ | ------------------ |
| INDEX   | *networkdevice_id* |
| INDEX   | *connectableci_id* |