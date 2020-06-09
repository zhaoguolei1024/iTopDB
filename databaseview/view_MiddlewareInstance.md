| 列                              | 类型                                         | 注释 |
| :------------------------------ | -------------------------------------------- | ---- |
| id                              | int [**0**]                                  |      |
| name                            | varchar(255) *NULL* []                       |      |
| description                     | text *NULL*                                  |      |
| org_id                          | int *NULL* [**0**]                           |      |
| organization_name               | varchar(255) *NULL* []                       |      |
| business_criticity              | enum('high','low','medium') *NULL* [**low**] |      |
| move2production                 | date *NULL*                                  |      |
| middleware_id                   | int *NULL* [**0**]                           |      |
| middleware_name                 | varchar(255) *NULL* []                       |      |
| finalclass                      | varchar(255) *NULL* [**FunctionalCI**]       |      |
| friendlyname                    | varchar(255) *NULL*                          |      |
| obsolescence_flag               | int [**0**]                                  |      |
| obsolescence_date               | date *NULL*                                  |      |
| org_id_friendlyname             | varchar(255) *NULL*                          |      |
| org_id_obsolescence_flag        | int [**0**]                                  |      |
| middleware_id_friendlyname      | varchar(511) *NULL*                          |      |
| middleware_id_obsolescence_flag | int [**0**]                                  |      |

```
select distinct `MiddlewareInstance`.`id` AS `id`,`MiddlewareInstance_FunctionalCI`.`name` AS `name`,`MiddlewareInstance_FunctionalCI`.`description` AS `description`,`MiddlewareInstance_FunctionalCI`.`org_id` AS `org_id`,`Organization_org_id`.`name` AS `organization_name`,`MiddlewareInstance_FunctionalCI`.`business_criticity` AS `business_criticity`,`MiddlewareInstance_FunctionalCI`.`move2production` AS `move2production`,`MiddlewareInstance`.`middleware_id` AS `middleware_id`,`Middleware_middleware_id_FunctionalCI`.`name` AS `middleware_name`,`MiddlewareInstance_FunctionalCI`.`finalclass` AS `finalclass`,cast(concat(coalesce(`MiddlewareInstance_FunctionalCI`.`name`,'')) as char charset utf8mb4) AS `friendlyname`,coalesce(coalesce((`Middleware_middleware_id_SoftwareInstance`.`status` = 'inactive'),0),0) AS `obsolescence_flag`,`MiddlewareInstance_FunctionalCI`.`obsolescence_date` AS `obsolescence_date`,cast(concat(coalesce(`Organization_org_id`.`name`,'')) as char charset utf8mb4) AS `org_id_friendlyname`,coalesce((`Organization_org_id`.`status` = 'inactive'),0) AS `org_id_obsolescence_flag`,cast(concat(coalesce(`Middleware_middleware_id_FunctionalCI`.`name`,''),coalesce(' ',''),coalesce(`FunctionalCI_system_id`.`name`,'')) as char charset utf8mb4) AS `middleware_id_friendlyname`,coalesce((`Middleware_middleware_id_SoftwareInstance`.`status` = 'inactive'),0) AS `middleware_id_obsolescence_flag` from ((`middlewareinstance` `MiddlewareInstance` join ((`softwareinstance` `Middleware_middleware_id_SoftwareInstance` join `functionalci` `FunctionalCI_system_id` on((`Middleware_middleware_id_SoftwareInstance`.`functionalci_id` = `FunctionalCI_system_id`.`id`))) join `functionalci` `Middleware_middleware_id_FunctionalCI` on((`Middleware_middleware_id_SoftwareInstance`.`id` = `Middleware_middleware_id_FunctionalCI`.`id`))) on((`MiddlewareInstance`.`middleware_id` = `Middleware_middleware_id_SoftwareInstance`.`id`))) join (`functionalci` `MiddlewareInstance_FunctionalCI` join `organization` `Organization_org_id` on((`MiddlewareInstance_FunctionalCI`.`org_id` = `Organization_org_id`.`id`))) on((`MiddlewareInstance`.`id` = `MiddlewareInstance_FunctionalCI`.`id`))) where (0 <> coalesce((`Middleware_middleware_id_SoftwareInstance`.`finalclass` = 'Middleware'),1))
```

