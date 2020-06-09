| 列                                   | 类型                                         | 注释 |
| :----------------------------------- | -------------------------------------------- | ---- |
| id                                   | int [**0**]                                  |      |
| name                                 | varchar(255) *NULL* []                       |      |
| description                          | text *NULL*                                  |      |
| org_id                               | int *NULL* [**0**]                           |      |
| organization_name                    | varchar(255) *NULL* []                       |      |
| business_criticity                   | enum('high','low','medium') *NULL* [**low**] |      |
| move2production                      | date *NULL*                                  |      |
| system_id                            | int *NULL* [**0**]                           |      |
| system_name                          | varchar(255) *NULL* []                       |      |
| software_id                          | int *NULL* [**0**]                           |      |
| software_name                        | varchar(255) *NULL* []                       |      |
| softwarelicence_id                   | int *NULL* [**0**]                           |      |
| softwarelicence_name                 | varchar(255) *NULL* []                       |      |
| path                                 | varchar(255) *NULL* []                       |      |
| status                               | enum('active','inactive') *NULL*             |      |
| finalclass                           | varchar(255) *NULL* [**FunctionalCI**]       |      |
| friendlyname                         | varchar(511) []                              |      |
| obsolescence_flag                    | int [**0**]                                  |      |
| obsolescence_date                    | date *NULL*                                  |      |
| org_id_friendlyname                  | varchar(255) []                              |      |
| org_id_obsolescence_flag             | int [**0**]                                  |      |
| system_id_friendlyname               | varchar(511) []                              |      |
| system_id_finalclass_recall          | varchar(255) *NULL* [**FunctionalCI**]       |      |
| system_id_obsolescence_flag          | int [**0**]                                  |      |
| software_id_friendlyname             | varchar(511) []                              |      |
| softwarelicence_id_friendlyname      | varchar(255) []                              |      |
| softwarelicence_id_obsolescence_flag | int [**0**]                                  |      |

```
select distinct `OtherSoftware_SoftwareInstance`.`id` AS `id`,`OtherSoftware_FunctionalCI`.`name` AS `name`,`OtherSoftware_FunctionalCI`.`description` AS `description`,`OtherSoftware_FunctionalCI`.`org_id` AS `org_id`,`Organization_org_id`.`name` AS `organization_name`,`OtherSoftware_FunctionalCI`.`business_criticity` AS `business_criticity`,`OtherSoftware_FunctionalCI`.`move2production` AS `move2production`,`OtherSoftware_SoftwareInstance`.`functionalci_id` AS `system_id`,`FunctionalCI_system_id`.`name` AS `system_name`,`OtherSoftware_SoftwareInstance`.`software_id` AS `software_id`,`Software_software_id`.`name` AS `software_name`,`OtherSoftware_SoftwareInstance`.`softwarelicence_id` AS `softwarelicence_id`,`SoftwareLicence_softwarelicence_id_Licence`.`name` AS `softwarelicence_name`,`OtherSoftware_SoftwareInstance`.`path` AS `path`,`OtherSoftware_SoftwareInstance`.`status` AS `status`,`OtherSoftware_FunctionalCI`.`finalclass` AS `finalclass`,cast(concat(coalesce(`OtherSoftware_FunctionalCI`.`name`,''),coalesce(' ',''),coalesce(`FunctionalCI_system_id`.`name`,'')) as char charset utf8mb4) AS `friendlyname`,coalesce((`OtherSoftware_SoftwareInstance`.`status` = 'inactive'),0) AS `obsolescence_flag`,`OtherSoftware_FunctionalCI`.`obsolescence_date` AS `obsolescence_date`,cast(concat(coalesce(`Organization_org_id`.`name`,'')) as char charset utf8mb4) AS `org_id_friendlyname`,coalesce((`Organization_org_id`.`status` = 'inactive'),0) AS `org_id_obsolescence_flag`,if((`FunctionalCI_system_id`.`finalclass` in ('Middleware','DBServer','WebServer','PCSoftware','OtherSoftware')),cast(concat(coalesce(`FunctionalCI_system_id`.`name`,''),coalesce(' ',''),coalesce(`FunctionalCI_system_id1`.`name`,'')) as char charset utf8mb4),cast(concat(coalesce(`FunctionalCI_system_id`.`name`,'')) as char charset utf8mb4)) AS `system_id_friendlyname`,`FunctionalCI_system_id`.`finalclass` AS `system_id_finalclass_recall`,if((`FunctionalCI_system_id`.`finalclass` = 'FunctionalCI'),coalesce(0,0),if((`FunctionalCI_system_id`.`finalclass` in ('Hypervisor','Farm','VirtualMachine')),coalesce((`FunctionalCI_system_id_poly_VirtualDevice`.`status` = 'obsolete'),0),if((`FunctionalCI_system_id`.`finalclass` = 'WebApplication'),coalesce(coalesce((`WebServer_webserver_id_SoftwareInstance`.`status` = 'inactive'),0),0),if((`FunctionalCI_system_id`.`finalclass` = 'DatabaseSchema'),coalesce(coalesce((`DBServer_dbserver_id_SoftwareInstance`.`status` = 'inactive'),0),0),if((`FunctionalCI_system_id`.`finalclass` = 'MiddlewareInstance'),coalesce(coalesce((`Middleware_middleware_id_SoftwareInstance`.`status` = 'inactive'),0),0),if((`FunctionalCI_system_id`.`finalclass` in ('Middleware','DBServer','WebServer','PCSoftware','OtherSoftware')),coalesce((`FunctionalCI_system_id_poly_SoftwareInstance`.`status` = 'inactive'),0),if((`FunctionalCI_system_id`.`finalclass` = 'BusinessProcess'),coalesce((`FunctionalCI_system_id_poly_BusinessProcess`.`status` = 'inactive'),0),if((`FunctionalCI_system_id`.`finalclass` = 'ApplicationSolution'),coalesce((`FunctionalCI_system_id_poly_ApplicationSolution`.`status` = 'inactive'),0),coalesce((`FunctionalCI_system_id_poly_PhysicalDevice`.`status` = 'obsolete'),0))))))))) AS `system_id_obsolescence_flag`,cast(concat(coalesce(`Software_software_id`.`name`,''),coalesce(' ',''),coalesce(`Software_software_id`.`version`,'')) as char charset utf8mb4) AS `software_id_friendlyname`,cast(concat(coalesce(`SoftwareLicence_softwarelicence_id_Licence`.`name`,'')) as char charset utf8mb4) AS `softwarelicence_id_friendlyname`,coalesce(((`SoftwareLicence_softwarelicence_id_Licence`.`perpetual` = 'no') and ((`SoftwareLicence_softwarelicence_id_Licence`.`end_date` is null) = 0) and (`SoftwareLicence_softwarelicence_id_Licence`.`end_date` < date_format((now() - interval 15 month),'%Y-%m-%d 00:00:00'))),0) AS `softwarelicence_id_obsolescence_flag` from ((((`softwareinstance` `OtherSoftware_SoftwareInstance` join ((((((((`functionalci` `FunctionalCI_system_id` left join (`softwareinstance` `FunctionalCI_system_id_poly_SoftwareInstance` join `functionalci` `FunctionalCI_system_id1` on((`FunctionalCI_system_id_poly_SoftwareInstance`.`functionalci_id` = `FunctionalCI_system_id1`.`id`))) on((`FunctionalCI_system_id`.`id` = `FunctionalCI_system_id_poly_SoftwareInstance`.`id`))) left join `virtualdevice` `FunctionalCI_system_id_poly_VirtualDevice` on((`FunctionalCI_system_id`.`id` = `FunctionalCI_system_id_poly_VirtualDevice`.`id`))) left join (`webapplication` `FunctionalCI_system_id_poly_WebApplication` join `softwareinstance` `WebServer_webserver_id_SoftwareInstance` on((`FunctionalCI_system_id_poly_WebApplication`.`webserver_id` = `WebServer_webserver_id_SoftwareInstance`.`id`))) on((`FunctionalCI_system_id`.`id` = `FunctionalCI_system_id_poly_WebApplication`.`id`))) left join (`databaseschema` `FunctionalCI_system_id_poly_DatabaseSchema` join `softwareinstance` `DBServer_dbserver_id_SoftwareInstance` on((`FunctionalCI_system_id_poly_DatabaseSchema`.`dbserver_id` = `DBServer_dbserver_id_SoftwareInstance`.`id`))) on((`FunctionalCI_system_id`.`id` = `FunctionalCI_system_id_poly_DatabaseSchema`.`id`))) left join (`middlewareinstance` `FunctionalCI_system_id_poly_MiddlewareInstance` join `softwareinstance` `Middleware_middleware_id_SoftwareInstance` on((`FunctionalCI_system_id_poly_MiddlewareInstance`.`middleware_id` = `Middleware_middleware_id_SoftwareInstance`.`id`))) on((`FunctionalCI_system_id`.`id` = `FunctionalCI_system_id_poly_MiddlewareInstance`.`id`))) left join `businessprocess` `FunctionalCI_system_id_poly_BusinessProcess` on((`FunctionalCI_system_id`.`id` = `FunctionalCI_system_id_poly_BusinessProcess`.`id`))) left join `applicationsolution` `FunctionalCI_system_id_poly_ApplicationSolution` on((`FunctionalCI_system_id`.`id` = `FunctionalCI_system_id_poly_ApplicationSolution`.`id`))) left join `physicaldevice` `FunctionalCI_system_id_poly_PhysicalDevice` on((`FunctionalCI_system_id`.`id` = `FunctionalCI_system_id_poly_PhysicalDevice`.`id`))) on((`OtherSoftware_SoftwareInstance`.`functionalci_id` = `FunctionalCI_system_id`.`id`))) left join `software` `Software_software_id` on((`OtherSoftware_SoftwareInstance`.`software_id` = `Software_software_id`.`id`))) left join `licence` `SoftwareLicence_softwarelicence_id_Licence` on((`OtherSoftware_SoftwareInstance`.`softwarelicence_id` = `SoftwareLicence_softwarelicence_id_Licence`.`id`))) join (`functionalci` `OtherSoftware_FunctionalCI` join `organization` `Organization_org_id` on((`OtherSoftware_FunctionalCI`.`org_id` = `Organization_org_id`.`id`))) on((`OtherSoftware_SoftwareInstance`.`id` = `OtherSoftware_FunctionalCI`.`id`))) where ((0 <> coalesce((`WebServer_webserver_id_SoftwareInstance`.`finalclass` = 'WebServer'),1)) and (0 <> coalesce((`DBServer_dbserver_id_SoftwareInstance`.`finalclass` = 'DBServer'),1)) and (0 <> coalesce((`Middleware_middleware_id_SoftwareInstance`.`finalclass` = 'Middleware'),1)) and (0 <> coalesce((`SoftwareLicence_softwarelicence_id_Licence`.`finalclass` = 'SoftwareLicence'),1)) and (0 <> coalesce((`OtherSoftware_SoftwareInstance`.`finalclass` = 'OtherSoftware'),1)))
```
