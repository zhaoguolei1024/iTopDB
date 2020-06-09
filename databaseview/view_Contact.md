|                          |                                               |      |
| :----------------------- | --------------------------------------------- | ---- |
| 列                       | 类型                                          | 注释 |
| id                       | int [**0**]                                   |      |
| name                     | varchar(255) *NULL* []                        |      |
| status                   | enum('active','inactive') *NULL* [**active**] |      |
| org_id                   | int *NULL* [**0**]                            |      |
| org_name                 | varchar(255) *NULL* []                        |      |
| email                    | varchar(255) *NULL* []                        |      |
| phone                    | varchar(255) *NULL* []                        |      |
| notify                   | enum('no','yes') *NULL* [**yes**]             |      |
| function                 | varchar(255) *NULL* []                        |      |
| finalclass               | varchar(255) *NULL* [**Contact**]             |      |
| friendlyname             | varchar(511) *NULL*                           |      |
| obsolescence_flag        | int [**0**]                                   |      |
| obsolescence_date        | date *NULL*                                   |      |
| org_id_friendlyname      | varchar(255) *NULL*                           |      |
| org_id_obsolescence_flag | int [**0**]                                   |      |

```
select distinct `Contact`.`id` AS `id`,`Contact`.`name` AS `name`,`Contact`.`status` AS `status`,`Contact`.`org_id` AS `org_id`,`Organization_org_id`.`name` AS `org_name`,`Contact`.`email` AS `email`,`Contact`.`phone` AS `phone`,`Contact`.`notify` AS `notify`,`Contact`.`function` AS `function`,`Contact`.`finalclass` AS `finalclass`,if((`Contact`.`finalclass` in ('Team','Contact')),cast(concat(coalesce(`Contact`.`name`,'')) as char charset utf8mb4),cast(concat(coalesce(`Contact_poly_Person`.`first_name`,''),coalesce(' ',''),coalesce(`Contact`.`name`,'')) as char charset utf8mb4)) AS `friendlyname`,coalesce((`Contact`.`status` = 'inactive'),0) AS `obsolescence_flag`,`Contact`.`obsolescence_date` AS `obsolescence_date`,cast(concat(coalesce(`Organization_org_id`.`name`,'')) as char charset utf8mb4) AS `org_id_friendlyname`,coalesce((`Organization_org_id`.`status` = 'inactive'),0) AS `org_id_obsolescence_flag` from ((`contact` `Contact` join `organization` `Organization_org_id` on((`Contact`.`org_id` = `Organization_org_id`.`id`))) left join `person` `Contact_poly_Person` on((`Contact`.`id` = `Contact_poly_Person`.`id`))) where (0 <> 1)
```

