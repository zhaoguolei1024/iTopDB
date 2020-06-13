model

拓扑 (Typology) >> Model

型号 (Model)



| 列       | 类型                                                         | 注释                                                         |
| :------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| id       | int *自动增量*                                               | 自增ID                                                       |
| brand_id | int *NULL* [**0**]                                           | 品牌                                                         |
| type     | enum('DiskArray','Enclosure','IPPhone','MobilePhone','NAS','NetworkDevice','PC','PDU','Peripheral','Phone','PowerSource','Printer','Rack','SANSwitch','Server','StorageSystem','Tablet','TapeLibrary') *NULL* | 设备类型，磁盘阵列 (DiskArray), 机位 (Enclosure), IP 电话 (IPPhone), 移动电话 (MobilePhone), NAS (NAS), 网络设备 (NetworkDevice), PC (PC), PDU (PDU), 配件 (Peripheral), 电话 (Phone), 电源 (PowerSource), 打印机 (Printer), 机柜 (Rack), SAN 交换机 (SANSwitch), 服务器 (Server), 存储系统 (StorageSystem), 平板 (Tablet), 磁带库 (TapeLibrary) |

### 索引

| PRIMARY | *id*       |
| :------ | ---------- |
| INDEX   | *brand_id* |