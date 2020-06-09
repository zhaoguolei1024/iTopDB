| 列       | 类型                                                         | 注释 |
| :------- | ------------------------------------------------------------ | ---- |
| id       | int *自动增量*                                               |      |
| brand_id | int *NULL* [**0**]                                           |      |
| type     | enum('DiskArray','Enclosure','IPPhone','MobilePhone','NAS','NetworkDevice','PC','PDU','Peripheral','Phone','PowerSource','Printer','Rack','SANSwitch','Server','StorageSystem','Tablet','TapeLibrary') *NULL* |      |

### 索引

| PRIMARY | *id*       |
| :------ | ---------- |
| INDEX   | *brand_id* |