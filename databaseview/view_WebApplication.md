| 列                             | 类型                                         | 注释 |
| :----------------------------- | -------------------------------------------- | ---- |
| id                             | int [**0**]                                  |      |
| name                           | varchar(255) *NULL* []                       |      |
| description                    | text *NULL*                                  |      |
| org_id                         | int *NULL* [**0**]                           |      |
| organization_name              | varchar(255) *NULL* []                       |      |
| business_criticity             | enum('high','low','medium') *NULL* [**low**] |      |
| move2production                | date *NULL*                                  |      |
| webserver_id                   | int *NULL* [**0**]                           |      |
| webserver_name                 | varchar(255) *NULL* []                       |      |
| url                            | varchar(2048) *NULL* []                      |      |
| finalclass                     | varchar(255) *NULL* [**FunctionalCI**]       |      |
| friendlyname                   | varchar(255) *NULL*                          |      |
| obsolescence_flag              | int [**0**]                                  |      |
| obsolescence_date              | date *NULL*                                  |      |
| org_id_friendlyname            | varchar(255) *NULL*                          |      |
| org_id_obsolescence_flag       | int [**0**]                                  |      |
| webserver_id_friendlyname      | varchar(511) *NULL*                          |      |
| webserver_id_obsolescence_flag | int [**0**]                                  |      |

```
select distinct `WebApplication`.`id` AS `id`,`WebApplication_FunctionalCI`.`name` AS `name`,`WebApplication_FunctionalCI`.`description` AS `description`,`WebApplication_FunctionalCI`.`org_id` AS `org_id`,`Organization_org_id`.`name` AS `organization_name`,`WebApplication_FunctionalCI`.`business_criticity` AS `business_criticity`,`WebApplication_FunctionalCI`.`move2production` AS `move2production`,`WebApplication`.`webserver_id` AS `webserver_id`,`WebServer_webserver_id_FunctionalCI`.`name` AS `webserver_name`,`WebApplication`.`url` AS `url`,`WebApplication_FunctionalCI`.`finalclass` AS `finalclass`,cast(concat(coalesce(`WebApplication_FunctionalCI`.`name`,'')) as char charset utf8mb4) AS `friendlyname`,coalesce(coalesce((`WebServer_webserver_id_SoftwareInstance`.`status` = 'inactive'),0),0) AS `obsolescence_flag`,`WebApplication_FunctionalCI`.`obsolescence_date` AS `obsolescence_date`,cast(concat(coalesce(`Organization_org_id`.`name`,'')) as char charset utf8mb4) AS `org_id_friendlyname`,coalesce((`Organization_org_id`.`status` = 'inactive'),0) AS `org_id_obsolescence_flag`,cast(concat(coalesce(`WebServer_webserver_id_FunctionalCI`.`name`,''),coalesce(' ',''),coalesce(`FunctionalCI_system_id`.`name`,'')) as char charset utf8mb4) AS `webserver_id_friendlyname`,coalesce((`WebServer_webserver_id_SoftwareInstance`.`status` = 'inactive'),0) AS `webserver_id_obsolescence_flag` from ((`webapplication` `WebApplication` join ((`softwareinstance` `WebServer_webserver_id_SoftwareInstance` join `functionalci` `FunctionalCI_system_id` on((`WebServer_webserver_id_SoftwareInstance`.`functionalci_id` = `FunctionalCI_system_id`.`id`))) join `functionalci` `WebServer_webserver_id_FunctionalCI` on((`WebServer_webserver_id_SoftwareInstance`.`id` = `WebServer_webserver_id_FunctionalCI`.`id`))) on((`WebApplication`.`webserver_id` = `WebServer_webserver_id_SoftwareInstance`.`id`))) join (`functionalci` `WebApplication_FunctionalCI` join `organization` `Organization_org_id` on((`WebApplication_FunctionalCI`.`org_id` = `Organization_org_id`.`id`))) on((`WebApplication`.`id` = `WebApplication_FunctionalCI`.`id`))) where (0 <> coalesce((`WebServer_webserver_id_SoftwareInstance`.`finalclass` = 'WebServer'),1))
```

