location

地理位置 (Location) - 任何类型的地理位置: 区域, 国家, 城市, 位置, 建筑, 楼层, 房间, 机架,...





| 列                | 类型                                          | 注释                                 |
| :---------------- | --------------------------------------------- | ------------------------------------ |
| id                | int *自动增量*                                | 自增ID                               |
| name              | varchar(255) *NULL* []                        | 属性编码                             |
| status            | enum('active','inactive') *NULL* [**active**] | 状态，启用 (active), 停用 (inactive) |
| org_id            | int *NULL* [**0**]                            | 拥有者组织                           |
| address           | text *NULL*                                   | 地址                                 |
| postal_code       | varchar(255) *NULL* []                        | 邮编                                 |
| city              | varchar(255) *NULL* []                        | 城市                                 |
| country           | varchar(255) *NULL* []                        | 国家                                 |
| obsolescence_date | date *NULL*                                   | 废弃时间                             |

### 索引

| PRIMARY | *id*       |
| :------ | ---------- |
| INDEX   | *name*(95) |
| INDEX   | *org_id*   |