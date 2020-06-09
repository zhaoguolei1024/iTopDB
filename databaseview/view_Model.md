| 列                    | 类型                                                         | 注释 |
| :-------------------- | ------------------------------------------------------------ | ---- |
| id                    | int [**0**]                                                  |      |
| name                  | varchar(255) *NULL* []                                       |      |
| brand_id              | int *NULL* [**0**]                                           |      |
| brand_name            | varchar(255) *NULL* []                                       |      |
| type                  | enum('DiskArray','Enclosure','IPPhone','MobilePhone','NAS','NetworkDevice','PC','PDU','Peripheral','Phone','PowerSource','Printer','Rack','SANSwitch','Server','StorageSystem','Tablet','TapeLibrary') *NULL* |      |
| finalclass            | varchar(255) *NULL* [**Typology**]                           |      |
| friendlyname          | varchar(255) *NULL*                                          |      |
| brand_id_friendlyname | varchar(255) *NULL*                                          |      |

```
select distinct `Model`.`id` AS `id`,`Model_Typology`.`name` AS `name`,`Model`.`brand_id` AS `brand_id`,`Brand_brand_id_Typology`.`name` AS `brand_name`,`Model`.`type` AS `type`,`Model_Typology`.`finalclass` AS `finalclass`,cast(concat(coalesce(`Model_Typology`.`name`,'')) as char charset utf8mb4) AS `friendlyname`,cast(concat(coalesce(`Brand_brand_id_Typology`.`name`,'')) as char charset utf8mb4) AS `brand_id_friendlyname` from ((`model` `Model` join `typology` `Brand_brand_id_Typology` on((`Model`.`brand_id` = `Brand_brand_id_Typology`.`id`))) join `typology` `Model_Typology` on((`Model`.`id` = `Model_Typology`.`id`))) where (0 <> coalesce((`Brand_brand_id_Typology`.`finalclass` = 'Brand'),1))
```

