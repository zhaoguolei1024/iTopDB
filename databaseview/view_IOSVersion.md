| 列                    | 类型                               | 注释 |
| :-------------------- | ---------------------------------- | ---- |
| id                    | int [**0**]                        |      |
| name                  | varchar(255) *NULL* []             |      |
| brand_id              | int *NULL* [**0**]                 |      |
| brand_name            | varchar(255) *NULL* []             |      |
| finalclass            | varchar(255) *NULL* [**Typology**] |      |
| friendlyname          | varchar(511) *NULL*                |      |
| brand_id_friendlyname | varchar(255) *NULL*                |      |

```
select distinct `IOSVersion`.`id` AS `id`,`IOSVersion_Typology`.`name` AS `name`,`IOSVersion`.`brand_id` AS `brand_id`,`Brand_brand_id_Typology`.`name` AS `brand_name`,`IOSVersion_Typology`.`finalclass` AS `finalclass`,cast(concat(coalesce(`Brand_brand_id_Typology`.`name`,''),coalesce(' ',''),coalesce(`IOSVersion_Typology`.`name`,'')) as char charset utf8mb4) AS `friendlyname`,cast(concat(coalesce(`Brand_brand_id_Typology`.`name`,'')) as char charset utf8mb4) AS `brand_id_friendlyname` from ((`iosversion` `IOSVersion` join `typology` `Brand_brand_id_Typology` on((`IOSVersion`.`brand_id` = `Brand_brand_id_Typology`.`id`))) join `typology` `IOSVersion_Typology` on((`IOSVersion`.`id` = `IOSVersion_Typology`.`id`))) where (0 <> coalesce((`Brand_brand_id_Typology`.`finalclass` = 'Brand'),1))
```

