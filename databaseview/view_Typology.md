| 列           | 类型                               | 注释 |
| :----------- | ---------------------------------- | ---- |
| id           | int [**0**]                        |      |
| name         | varchar(255) *NULL* []             |      |
| finalclass   | varchar(255) *NULL* [**Typology**] |      |
| friendlyname | varchar(511) *NULL*                |      |

```
select distinct `Typology`.`id` AS `id`,`Typology`.`name` AS `name`,`Typology`.`finalclass` AS `finalclass`,if((`Typology`.`finalclass` = 'IOSVersion'),cast(concat(coalesce(`Brand_brand_id_Typology`.`name`,''),coalesce(' ',''),coalesce(`Typology`.`name`,'')) as char charset utf8mb4),cast(concat(coalesce(`Typology`.`name`,'')) as char charset utf8mb4)) AS `friendlyname` from (`typology` `Typology` left join (`iosversion` `Typology_poly_IOSVersion` join `typology` `Brand_brand_id_Typology` on((`Typology_poly_IOSVersion`.`brand_id` = `Brand_brand_id_Typology`.`id`))) on((`Typology`.`id` = `Typology_poly_IOSVersion`.`id`))) where (0 <> coalesce((`Brand_brand_id_Typology`.`finalclass` = 'Brand'),1))
```

