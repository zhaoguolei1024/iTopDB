| 列                       | 类型                            | 注释 |
| :----------------------- | ------------------------------- | ---- |
| id                       | int [**0**]                     |      |
| name                     | varchar(255) *NULL* []          |      |
| description              | text *NULL*                     |      |
| software_id              | int *NULL* [**0**]              |      |
| software_name            | varchar(255) *NULL* []          |      |
| finalclass               | varchar(255) *NULL* [**Patch**] |      |
| friendlyname             | varchar(255) *NULL*             |      |
| software_id_friendlyname | varchar(511) *NULL*             |      |

```
select distinct `SoftwarePatch`.`id` AS `id`,`SoftwarePatch_Patch`.`name` AS `name`,`SoftwarePatch_Patch`.`description` AS `description`,`SoftwarePatch`.`software_id` AS `software_id`,`Software_software_id`.`name` AS `software_name`,`SoftwarePatch_Patch`.`finalclass` AS `finalclass`,cast(concat(coalesce(`SoftwarePatch_Patch`.`name`,'')) as char charset utf8mb4) AS `friendlyname`,cast(concat(coalesce(`Software_software_id`.`name`,''),coalesce(' ',''),coalesce(`Software_software_id`.`version`,'')) as char charset utf8mb4) AS `software_id_friendlyname` from ((`softwarepatch` `SoftwarePatch` join `software` `Software_software_id` on((`SoftwarePatch`.`software_id` = `Software_software_id`.`id`))) join `patch` `SoftwarePatch_Patch` on((`SoftwarePatch`.`id` = `SoftwarePatch_Patch`.`id`))) where (0 <> 1)
```

