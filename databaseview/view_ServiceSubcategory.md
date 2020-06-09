| 列                               | 类型                                                     | 注释 |
| :------------------------------- | -------------------------------------------------------- | ---- |
| id                               | int [**0**]                                              |      |
| name                             | varchar(255) *NULL* []                                   |      |
| description                      | text *NULL*                                              |      |
| service_id                       | int *NULL* [**0**]                                       |      |
| service_org_id                   | int *NULL* [**0**]                                       |      |
| service_name                     | varchar(255) *NULL* []                                   |      |
| service_provider                 | varchar(255) *NULL* []                                   |      |
| request_type                     | enum('incident','service_request') *NULL* [**incident**] |      |
| status                           | enum('implementation','obsolete','production') *NULL*    |      |
| friendlyname                     | varchar(255) *NULL*                                      |      |
| service_id_friendlyname          | varchar(255) *NULL*                                      |      |
| service_org_id_friendlyname      | varchar(255) *NULL*                                      |      |
| service_org_id_obsolescence_flag | int [**0**]                                              |      |

```
select distinct `ServiceSubcategory`.`id` AS `id`,`ServiceSubcategory`.`name` AS `name`,`ServiceSubcategory`.`description` AS `description`,`ServiceSubcategory`.`service_id` AS `service_id`,`Service_service_id`.`org_id` AS `service_org_id`,`Service_service_id`.`name` AS `service_name`,`Organization_org_id`.`name` AS `service_provider`,`ServiceSubcategory`.`request_type` AS `request_type`,`ServiceSubcategory`.`status` AS `status`,cast(concat(coalesce(`ServiceSubcategory`.`name`,'')) as char charset utf8mb4) AS `friendlyname`,cast(concat(coalesce(`Service_service_id`.`name`,'')) as char charset utf8mb4) AS `service_id_friendlyname`,cast(concat(coalesce(`Organization_org_id`.`name`,'')) as char charset utf8mb4) AS `service_org_id_friendlyname`,coalesce((`Organization_org_id`.`status` = 'inactive'),0) AS `service_org_id_obsolescence_flag` from (`servicesubcategory` `ServiceSubcategory` join (`service` `Service_service_id` join `organization` `Organization_org_id` on((`Service_service_id`.`org_id` = `Organization_org_id`.`id`))) on((`ServiceSubcategory`.`service_id` = `Service_service_id`.`id`))) where (0 <> 1)
```

