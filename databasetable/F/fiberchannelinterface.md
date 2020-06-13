fiberchannelinterface

光纤通道接口 (FiberChannelInterface)

网卡 (NetworkInterface) >> FiberChannelInterface



| 列                  | 类型                   | 注释   |
| :------------------ | ---------------------- | ------ |
| id                  | int *自动增量*         | 自增ID |
| speed               | decimal(6,2) *NULL*    | 速率   |
| topology            | varchar(255) *NULL* [] | 拓扑   |
| wwn                 | varchar(255) *NULL* [] | WWN    |
| datacenterdevice_id | int *NULL* [**0**]     | 设备   |

### 索引

| PRIMARY | *id*                  |
| :------ | --------------------- |
| INDEX   | *datacenterdevice_id* |