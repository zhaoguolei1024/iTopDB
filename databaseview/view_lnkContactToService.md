| 列                           | 类型                              | 注释 |
| :--------------------------- | --------------------------------- | ---- |
| id                           | int [**0**]                       |      |
| service_id                   | int *NULL* [**0**]                |      |
| service_name                 | varchar(255) *NULL* []            |      |
| contact_id                   | int *NULL* [**0**]                |      |
| contact_name                 | varchar(255) *NULL* []            |      |
| friendlyname                 | varchar(23) *NULL*                |      |
| service_id_friendlyname      | varchar(255) *NULL*               |      |
| contact_id_friendlyname      | varchar(511) *NULL*               |      |
| contact_id_finalclass_recall | varchar(255) *NULL* [**Contact**] |      |
| contact_id_obsolescence_flag | int [**0**]                       |      |

```
select distinct `lnkContactToService`.`id` AS `id`,`lnkContactToService`.`service_id` AS `service_id`,`Service_service_id`.`name` AS `service_name`,`lnkContactToService`.`contact_id` AS `contact_id`,`Contact_contact_id`.`name` AS `contact_name`,cast(concat(coalesce(`lnkContactToService`.`service_id`,''),coalesce(' ',''),coalesce(`lnkContactToService`.`contact_id`,'')) as char charset utf8mb4) AS `friendlyname`,cast(concat(coalesce(`Service_service_id`.`name`,'')) as char charset utf8mb4) AS `service_id_friendlyname`,if((`Contact_contact_id`.`finalclass` in ('Team','Contact')),cast(concat(coalesce(`Contact_contact_id`.`name`,'')) as char charset utf8mb4),cast(concat(coalesce(`Contact_contact_id_poly_Person`.`first_name`,''),coalesce(' ',''),coalesce(`Contact_contact_id`.`name`,'')) as char charset utf8mb4)) AS `contact_id_friendlyname`,`Contact_contact_id`.`finalclass` AS `contact_id_finalclass_recall`,coalesce((`Contact_contact_id`.`status` = 'inactive'),0) AS `contact_id_obsolescence_flag` from ((`lnkcontacttoservice` `lnkContactToService` join `service` `Service_service_id` on((`lnkContactToService`.`service_id` = `Service_service_id`.`id`))) join (`contact` `Contact_contact_id` left join `person` `Contact_contact_id_poly_Person` on((`Contact_contact_id`.`id` = `Contact_contact_id_poly_Person`.`id`))) on((`lnkContactToService`.`contact_id` = `Contact_contact_id`.`id`))) where (0 <> 1)
```

