| 列                            | 类型                                         | 注释 |
| :---------------------------- | -------------------------------------------- | ---- |
| id                            | int [**0**]                                  |      |
| name                          | varchar(255) *NULL* []                       |      |
| description                   | text *NULL*                                  |      |
| org_id                        | int *NULL* [**0**]                           |      |
| organization_name             | varchar(255) *NULL* []                       |      |
| business_criticity            | enum('high','low','medium') *NULL* [**low**] |      |
| move2production               | date *NULL*                                  |      |
| dbserver_id                   | int *NULL* [**0**]                           |      |
| dbserver_name                 | varchar(255) *NULL* []                       |      |
| finalclass                    | varchar(255) *NULL* [**FunctionalCI**]       |      |
| friendlyname                  | varchar(255) *NULL*                          |      |
| obsolescence_flag             | int [**0**]                                  |      |
| obsolescence_date             | date *NULL*                                  |      |
| org_id_friendlyname           | varchar(255) *NULL*                          |      |
| org_id_obsolescence_flag      | int [**0**]                                  |      |
| dbserver_id_friendlyname      | varchar(511) *NULL*                          |      |
| dbserver_id_obsolescence_flag | int [**0**]                                  |      |

```
select distinct `DatabaseSchema`.`id` AS `id`,`DatabaseSchema_FunctionalCI`.`name` AS `name`,`DatabaseSchema_FunctionalCI`.`description` AS `description`,`DatabaseSchema_FunctionalCI`.`org_id` AS `org_id`,`Organization_org_id`.`name` AS `organization_name`,`DatabaseSchema_FunctionalCI`.`business_criticity` AS `business_criticity`,`DatabaseSchema_FunctionalCI`.`move2production` AS `move2production`,`DatabaseSchema`.`dbserver_id` AS `dbserver_id`,`DBServer_dbserver_id_FunctionalCI`.`name` AS `dbserver_name`,`DatabaseSchema_FunctionalCI`.`finalclass` AS `finalclass`,cast(concat(coalesce(`DatabaseSchema_FunctionalCI`.`name`,'')) as char charset utf8mb4) AS `friendlyname`,coalesce(coalesce((`DBServer_dbserver_id_SoftwareInstance`.`status` = 'inactive'),0),0) AS `obsolescence_flag`,`DatabaseSchema_FunctionalCI`.`obsolescence_date` AS `obsolescence_date`,cast(concat(coalesce(`Organization_org_id`.`name`,'')) as char charset utf8mb4) AS `org_id_friendlyname`,coalesce((`Organization_org_id`.`status` = 'inactive'),0) AS `org_id_obsolescence_flag`,cast(concat(coalesce(`DBServer_dbserver_id_FunctionalCI`.`name`,''),coalesce(' ',''),coalesce(`FunctionalCI_system_id`.`name`,'')) as char charset utf8mb4) AS `dbserver_id_friendlyname`,coalesce((`DBServer_dbserver_id_SoftwareInstance`.`status` = 'inactive'),0) AS `dbserver_id_obsolescence_flag` from ((`databaseschema` `DatabaseSchema` join ((`softwareinstance` `DBServer_dbserver_id_SoftwareInstance` join `functionalci` `FunctionalCI_system_id` on((`DBServer_dbserver_id_SoftwareInstance`.`functionalci_id` = `FunctionalCI_system_id`.`id`))) join `functionalci` `DBServer_dbserver_id_FunctionalCI` on((`DBServer_dbserver_id_SoftwareInstance`.`id` = `DBServer_dbserver_id_FunctionalCI`.`id`))) on((`DatabaseSchema`.`dbserver_id` = `DBServer_dbserver_id_SoftwareInstance`.`id`))) join (`functionalci` `DatabaseSchema_FunctionalCI` join `organization` `Organization_org_id` on((`DatabaseSchema_FunctionalCI`.`org_id` = `Organization_org_id`.`id`))) on((`DatabaseSchema`.`id` = `DatabaseSchema_FunctionalCI`.`id`))) where (0 <> coalesce((`DBServer_dbserver_id_SoftwareInstance`.`finalclass` = 'DBServer'),1))
```

