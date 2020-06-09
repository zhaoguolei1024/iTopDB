| 列                       | 类型                   | 注释 |
| :----------------------- | ---------------------- | ---- |
| id                       | int [**0**]            |      |
| description              | text *NULL*            |      |
| subnet_name              | varchar(255) *NULL* [] |      |
| org_id                   | int *NULL* [**0**]     |      |
| org_name                 | varchar(255) *NULL* [] |      |
| ip                       | varchar(255) *NULL* [] |      |
| ip_mask                  | varchar(255) *NULL* [] |      |
| friendlyname             | varchar(511) *NULL*    |      |
| org_id_friendlyname      | varchar(255) *NULL*    |      |
| org_id_obsolescence_flag | int [**0**]            |      |

```
select distinct `Subnet`.`id` AS `id`,`Subnet`.`description` AS `description`,`Subnet`.`subnet_name` AS `subnet_name`,`Subnet`.`org_id` AS `org_id`,`Organization_org_id`.`name` AS `org_name`,`Subnet`.`ip` AS `ip`,`Subnet`.`ip_mask` AS `ip_mask`,cast(concat(coalesce(`Subnet`.`ip`,''),coalesce(' ',''),coalesce(`Subnet`.`ip_mask`,'')) as char charset utf8mb4) AS `friendlyname`,cast(concat(coalesce(`Organization_org_id`.`name`,'')) as char charset utf8mb4) AS `org_id_friendlyname`,coalesce((`Organization_org_id`.`status` = 'inactive'),0) AS `org_id_obsolescence_flag` from (`subnet` `Subnet` join `organization` `Organization_org_id` on((`Subnet`.`org_id` = `Organization_org_id`.`id`))) where (0 <> 1)
```

