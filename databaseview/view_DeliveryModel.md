| 列                       | 类型                   | 注释 |
| :----------------------- | ---------------------- | ---- |
| id                       | int [**0**]            |      |
| name                     | varchar(255) *NULL* [] |      |
| org_id                   | int *NULL* [**0**]     |      |
| organization_name        | varchar(255) *NULL* [] |      |
| description              | text *NULL*            |      |
| friendlyname             | varchar(255) *NULL*    |      |
| org_id_friendlyname      | varchar(255) *NULL*    |      |
| org_id_obsolescence_flag | int [**0**]            |      |

```
select distinct `DeliveryModel`.`id` AS `id`,`DeliveryModel`.`name` AS `name`,`DeliveryModel`.`org_id` AS `org_id`,`Organization_org_id`.`name` AS `organization_name`,`DeliveryModel`.`description` AS `description`,cast(concat(coalesce(`DeliveryModel`.`name`,'')) as char charset utf8mb4) AS `friendlyname`,cast(concat(coalesce(`Organization_org_id`.`name`,'')) as char charset utf8mb4) AS `org_id_friendlyname`,coalesce((`Organization_org_id`.`status` = 'inactive'),0) AS `org_id_obsolescence_flag` from (`deliverymodel` `DeliveryModel` join `organization` `Organization_org_id` on((`DeliveryModel`.`org_id` = `Organization_org_id`.`id`))) where (0 <> 1)
```

