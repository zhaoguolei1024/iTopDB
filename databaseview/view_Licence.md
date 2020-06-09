| 列                       | 类型                              | 注释 |
| :----------------------- | --------------------------------- | ---- |
| id                       | int [**0**]                       |      |
| name                     | varchar(255) *NULL* []            |      |
| org_id                   | int *NULL* [**0**]                |      |
| organization_name        | varchar(255) *NULL* []            |      |
| usage_limit              | varchar(255) *NULL* []            |      |
| description              | text *NULL*                       |      |
| start_date               | date *NULL*                       |      |
| end_date                 | date *NULL*                       |      |
| licence_key              | varchar(255) *NULL* []            |      |
| perpetual                | enum('no','yes') *NULL* [**no**]  |      |
| finalclass               | varchar(255) *NULL* [**Licence**] |      |
| friendlyname             | varchar(255) *NULL*               |      |
| obsolescence_flag        | int [**0**]                       |      |
| obsolescence_date        | date *NULL*                       |      |
| org_id_friendlyname      | varchar(255) *NULL*               |      |
| org_id_obsolescence_flag | int [**0**]                       |      |

```
select distinct `Licence`.`id` AS `id`,`Licence`.`name` AS `name`,`Licence`.`org_id` AS `org_id`,`Organization_org_id`.`name` AS `organization_name`,`Licence`.`usage_limit` AS `usage_limit`,`Licence`.`description` AS `description`,`Licence`.`start_date` AS `start_date`,`Licence`.`end_date` AS `end_date`,`Licence`.`licence_key` AS `licence_key`,`Licence`.`perpetual` AS `perpetual`,`Licence`.`finalclass` AS `finalclass`,cast(concat(coalesce(`Licence`.`name`,'')) as char charset utf8mb4) AS `friendlyname`,coalesce(((`Licence`.`perpetual` = 'no') and ((`Licence`.`end_date` is null) = 0) and (`Licence`.`end_date` < date_format((now() - interval 15 month),'%Y-%m-%d 00:00:00'))),0) AS `obsolescence_flag`,`Licence`.`obsolescence_date` AS `obsolescence_date`,cast(concat(coalesce(`Organization_org_id`.`name`,'')) as char charset utf8mb4) AS `org_id_friendlyname`,coalesce((`Organization_org_id`.`status` = 'inactive'),0) AS `org_id_obsolescence_flag` from (`licence` `Licence` join `organization` `Organization_org_id` on((`Licence`.`org_id` = `Organization_org_id`.`id`))) where (0 <> 1)
```

