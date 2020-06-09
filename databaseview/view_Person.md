| 列                            | 类型                                          | 注释 |
| :---------------------------- | --------------------------------------------- | ---- |
| id                            | int [**0**]                                   |      |
| name                          | varchar(255) *NULL* []                        |      |
| status                        | enum('active','inactive') *NULL* [**active**] |      |
| org_id                        | int *NULL* [**0**]                            |      |
| org_name                      | varchar(255) *NULL* []                        |      |
| email                         | varchar(255) *NULL* []                        |      |
| phone                         | varchar(255) *NULL* []                        |      |
| notify                        | enum('no','yes') *NULL* [**yes**]             |      |
| function                      | varchar(255) *NULL* []                        |      |
| picture                       | varchar(255) *NULL*                           |      |
| first_name                    | varchar(255) *NULL* []                        |      |
| employee_number               | varchar(255) *NULL* []                        |      |
| mobile_phone                  | varchar(255) *NULL* []                        |      |
| location_id                   | int *NULL* [**0**]                            |      |
| location_name                 | varchar(255) *NULL* []                        |      |
| manager_id                    | int *NULL* [**0**]                            |      |
| manager_name                  | varchar(255) *NULL* []                        |      |
| finalclass                    | varchar(255) *NULL* [**Contact**]             |      |
| friendlyname                  | varchar(511) *NULL*                           |      |
| obsolescence_flag             | int [**0**]                                   |      |
| obsolescence_date             | date *NULL*                                   |      |
| org_id_friendlyname           | varchar(255) *NULL*                           |      |
| org_id_obsolescence_flag      | int [**0**]                                   |      |
| location_id_friendlyname      | varchar(255) *NULL*                           |      |
| location_id_obsolescence_flag | int [**0**]                                   |      |
| manager_id_friendlyname       | varchar(511) *NULL*                           |      |
| manager_id_obsolescence_flag  | int [**0**]                                   |      |
| Personpicture_data            | longblob *NULL*                               |      |
| Personpicture_filename        | varchar(255) *NULL*                           |      |

```
select distinct `Person`.`id` AS `id`,`Person_Contact`.`name` AS `name`,`Person_Contact`.`status` AS `status`,`Person_Contact`.`org_id` AS `org_id`,`Organization_org_id`.`name` AS `org_name`,`Person_Contact`.`email` AS `email`,`Person_Contact`.`phone` AS `phone`,`Person_Contact`.`notify` AS `notify`,`Person_Contact`.`function` AS `function`,`Person`.`picture_mimetype` AS `picture`,`Person`.`first_name` AS `first_name`,`Person`.`employee_number` AS `employee_number`,`Person`.`mobile_phone` AS `mobile_phone`,`Person`.`location_id` AS `location_id`,`Location_location_id`.`name` AS `location_name`,`Person`.`manager_id` AS `manager_id`,`Person_manager_id_Contact`.`name` AS `manager_name`,`Person_Contact`.`finalclass` AS `finalclass`,cast(concat(coalesce(`Person`.`first_name`,''),coalesce(' ',''),coalesce(`Person_Contact`.`name`,'')) as char charset utf8mb4) AS `friendlyname`,coalesce((`Person_Contact`.`status` = 'inactive'),0) AS `obsolescence_flag`,`Person_Contact`.`obsolescence_date` AS `obsolescence_date`,cast(concat(coalesce(`Organization_org_id`.`name`,'')) as char charset utf8mb4) AS `org_id_friendlyname`,coalesce((`Organization_org_id`.`status` = 'inactive'),0) AS `org_id_obsolescence_flag`,cast(concat(coalesce(`Location_location_id`.`name`,'')) as char charset utf8mb4) AS `location_id_friendlyname`,coalesce((`Location_location_id`.`status` = 'inactive'),0) AS `location_id_obsolescence_flag`,cast(concat(coalesce(`Person_manager_id`.`first_name`,''),coalesce(' ',''),coalesce(`Person_manager_id_Contact`.`name`,'')) as char charset utf8mb4) AS `manager_id_friendlyname`,coalesce((`Person_manager_id_Contact`.`status` = 'inactive'),0) AS `manager_id_obsolescence_flag`,`Person`.`picture_data` AS `Personpicture_data`,`Person`.`picture_filename` AS `Personpicture_filename` from (((`person` `Person` left join `location` `Location_location_id` on((`Person`.`location_id` = `Location_location_id`.`id`))) left join (`person` `Person_manager_id` join `contact` `Person_manager_id_Contact` on((`Person_manager_id`.`id` = `Person_manager_id_Contact`.`id`))) on((`Person`.`manager_id` = `Person_manager_id`.`id`))) join (`contact` `Person_Contact` join `organization` `Organization_org_id` on((`Person_Contact`.`org_id` = `Organization_org_id`.`id`))) on((`Person`.`id` = `Person_Contact`.`id`))) where (0 <> 1)
```

