| 列                       | 类型                               | 注释 |
| :----------------------- | ---------------------------------- | ---- |
| id                       | int [**0**]                        |      |
| name                     | varchar(255) *NULL* []             |      |
| osfamily_id              | int *NULL* [**0**]                 |      |
| osfamily_name            | varchar(255) *NULL* []             |      |
| finalclass               | varchar(255) *NULL* [**Typology**] |      |
| friendlyname             | varchar(255) *NULL*                |      |
| osfamily_id_friendlyname | varchar(255) *NULL*                |      |

```
select distinct `OSVersion`.`id` AS `id`,`OSVersion_Typology`.`name` AS `name`,`OSVersion`.`osfamily_id` AS `osfamily_id`,`OSFamily_osfamily_id_Typology`.`name` AS `osfamily_name`,`OSVersion_Typology`.`finalclass` AS `finalclass`,cast(concat(coalesce(`OSVersion_Typology`.`name`,'')) as char charset utf8mb4) AS `friendlyname`,cast(concat(coalesce(`OSFamily_osfamily_id_Typology`.`name`,'')) as char charset utf8mb4) AS `osfamily_id_friendlyname` from ((`osversion` `OSVersion` join `typology` `OSFamily_osfamily_id_Typology` on((`OSVersion`.`osfamily_id` = `OSFamily_osfamily_id_Typology`.`id`))) join `typology` `OSVersion_Typology` on((`OSVersion`.`id` = `OSVersion_Typology`.`id`))) where (0 <> coalesce((`OSFamily_osfamily_id_Typology`.`finalclass` = 'OSFamily'),1))
```

