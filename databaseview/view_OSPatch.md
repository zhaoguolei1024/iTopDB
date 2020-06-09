| 列                        | 类型                            | 注释 |
| :------------------------ | ------------------------------- | ---- |
| id                        | int [**0**]                     |      |
| name                      | varchar(255) *NULL* []          |      |
| description               | text *NULL*                     |      |
| osversion_id              | int *NULL* [**0**]              |      |
| osversion_name            | varchar(255) *NULL* []          |      |
| finalclass                | varchar(255) *NULL* [**Patch**] |      |
| friendlyname              | varchar(255) *NULL*             |      |
| osversion_id_friendlyname | varchar(255) *NULL*             |      |

```
select distinct `OSPatch`.`id` AS `id`,`OSPatch_Patch`.`name` AS `name`,`OSPatch_Patch`.`description` AS `description`,`OSPatch`.`osversion_id` AS `osversion_id`,`OSVersion_osversion_id_Typology`.`name` AS `osversion_name`,`OSPatch_Patch`.`finalclass` AS `finalclass`,cast(concat(coalesce(`OSPatch_Patch`.`name`,'')) as char charset utf8mb4) AS `friendlyname`,cast(concat(coalesce(`OSVersion_osversion_id_Typology`.`name`,'')) as char charset utf8mb4) AS `osversion_id_friendlyname` from ((`ospatch` `OSPatch` join `typology` `OSVersion_osversion_id_Typology` on((`OSPatch`.`osversion_id` = `OSVersion_osversion_id_Typology`.`id`))) join `patch` `OSPatch_Patch` on((`OSPatch`.`id` = `OSPatch_Patch`.`id`))) where (0 <> coalesce((`OSVersion_osversion_id_Typology`.`finalclass` = 'OSVersion'),1))
```

