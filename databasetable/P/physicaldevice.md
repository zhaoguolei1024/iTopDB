| 列              | 类型                                                         | 注释 |
| :-------------- | ------------------------------------------------------------ | ---- |
| id              | int *自动增量*                                               |      |
| serialnumber    | varchar(255) *NULL* []                                       |      |
| location_id     | int *NULL* [**0**]                                           |      |
| status          | enum('implementation','obsolete','production','stock') *NULL* [**production**] |      |
| brand_id        | int *NULL* [**0**]                                           |      |
| model_id        | int *NULL* [**0**]                                           |      |
| asset_number    | varchar(255) *NULL* []                                       |      |
| purchase_date   | date *NULL*                                                  |      |
| end_of_warranty | date *NULL*                                                  |      |
| finalclass      | varchar(255) *NULL* [**PhysicalDevice**]                     |      |

### 索引

| PRIMARY | *id*             |
| :------ | ---------------- |
| INDEX   | *location_id*    |
| INDEX   | *brand_id*       |
| INDEX   | *model_id*       |
| INDEX   | *finalclass*(95) |