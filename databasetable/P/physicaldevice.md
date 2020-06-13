physicaldevice

物理设备 (PhysicalDevice)

功能配置项 (FunctionalCI) >> PhysicalDevice



| 列              | 类型                                                         | 注释                                                         |
| :-------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| id              | int *自动增量*                                               | 自增ID                                                       |
| serialnumber    | varchar(255) *NULL* []                                       | 序列号                                                       |
| location_id     | int *NULL* [**0**]                                           | 地理位置                                                     |
| status          | enum('implementation','obsolete','production','stock') *NULL* [**production**] | 状态，上线 (implementation), 废弃 (obsolete), 生产 (production), 闲置 (stock) |
| brand_id        | int *NULL* [**0**]                                           | 品牌                                                         |
| model_id        | int *NULL* [**0**]                                           | 型号                                                         |
| asset_number    | varchar(255) *NULL* []                                       | 资产编号                                                     |
| purchase_date   | date *NULL*                                                  | 采购日期                                                     |
| end_of_warranty | date *NULL*                                                  | 过保日期                                                     |
| finalclass      | varchar(255) *NULL* [**PhysicalDevice**]                     | 二级配置项                                                   |

### 索引

| PRIMARY | *id*             |
| :------ | ---------------- |
| INDEX   | *location_id*    |
| INDEX   | *brand_id*       |
| INDEX   | *model_id*       |
| INDEX   | *finalclass*(95) |