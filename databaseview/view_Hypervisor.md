| 列                          | 类型                                                         | 注释 |
| :-------------------------- | ------------------------------------------------------------ | ---- |
| id                          | int [**0**]                                                  |      |
| name                        | varchar(255) *NULL* []                                       |      |
| description                 | text *NULL*                                                  |      |
| org_id                      | int *NULL* [**0**]                                           |      |
| organization_name           | varchar(255) *NULL* []                                       |      |
| business_criticity          | enum('high','low','medium') *NULL* [**low**]                 |      |
| move2production             | date *NULL*                                                  |      |
| status                      | enum('implementation','obsolete','production','stock') *NULL* [**production**] |      |
| farm_id                     | int *NULL* [**0**]                                           |      |
| farm_name                   | varchar(255) *NULL* []                                       |      |
| server_id                   | int *NULL* [**0**]                                           |      |
| server_name                 | varchar(255) *NULL* []                                       |      |
| finalclass                  | varchar(255) *NULL* [**FunctionalCI**]                       |      |
| friendlyname                | varchar(255) *NULL*                                          |      |
| obsolescence_flag           | int [**0**]                                                  |      |
| obsolescence_date           | date *NULL*                                                  |      |
| org_id_friendlyname         | varchar(255) *NULL*                                          |      |
| org_id_obsolescence_flag    | int [**0**]                                                  |      |
| farm_id_friendlyname        | varchar(255) *NULL*                                          |      |
| farm_id_obsolescence_flag   | int [**0**]                                                  |      |
| server_id_friendlyname      | varchar(255) *NULL*                                          |      |
| server_id_obsolescence_flag | int [**0**]                                                  |      |

```
select distinct `Hypervisor`.`id` AS `id`,`Hypervisor_FunctionalCI`.`name` AS `name`,`Hypervisor_FunctionalCI`.`description` AS `description`,`Hypervisor_FunctionalCI`.`org_id` AS `org_id`,`Organization_org_id`.`name` AS `organization_name`,`Hypervisor_FunctionalCI`.`business_criticity` AS `business_criticity`,`Hypervisor_FunctionalCI`.`move2production` AS `move2production`,`Hypervisor_VirtualDevice`.`status` AS `status`,`Hypervisor`.`farm_id` AS `farm_id`,`Farm_farm_id_FunctionalCI`.`name` AS `farm_name`,`Hypervisor`.`server_id` AS `server_id`,`Server_server_id_FunctionalCI`.`name` AS `server_name`,`Hypervisor_FunctionalCI`.`finalclass` AS `finalclass`,cast(concat(coalesce(`Hypervisor_FunctionalCI`.`name`,'')) as char charset utf8mb4) AS `friendlyname`,coalesce((`Hypervisor_VirtualDevice`.`status` = 'obsolete'),0) AS `obsolescence_flag`,`Hypervisor_FunctionalCI`.`obsolescence_date` AS `obsolescence_date`,cast(concat(coalesce(`Organization_org_id`.`name`,'')) as char charset utf8mb4) AS `org_id_friendlyname`,coalesce((`Organization_org_id`.`status` = 'inactive'),0) AS `org_id_obsolescence_flag`,cast(concat(coalesce(`Farm_farm_id_FunctionalCI`.`name`,'')) as char charset utf8mb4) AS `farm_id_friendlyname`,coalesce((`Farm_farm_id_VirtualDevice`.`status` = 'obsolete'),0) AS `farm_id_obsolescence_flag`,cast(concat(coalesce(`Server_server_id_FunctionalCI`.`name`,'')) as char charset utf8mb4) AS `server_id_friendlyname`,coalesce((`Server_server_id_PhysicalDevice`.`status` = 'obsolete'),0) AS `server_id_obsolescence_flag` from ((((`hypervisor` `Hypervisor` left join (`virtualdevice` `Farm_farm_id_VirtualDevice` join `functionalci` `Farm_farm_id_FunctionalCI` on((`Farm_farm_id_VirtualDevice`.`id` = `Farm_farm_id_FunctionalCI`.`id`))) on((`Hypervisor`.`farm_id` = `Farm_farm_id_VirtualDevice`.`id`))) left join (`physicaldevice` `Server_server_id_PhysicalDevice` join `functionalci` `Server_server_id_FunctionalCI` on((`Server_server_id_PhysicalDevice`.`id` = `Server_server_id_FunctionalCI`.`id`))) on((`Hypervisor`.`server_id` = `Server_server_id_PhysicalDevice`.`id`))) join `virtualdevice` `Hypervisor_VirtualDevice` on((`Hypervisor`.`id` = `Hypervisor_VirtualDevice`.`id`))) join (`functionalci` `Hypervisor_FunctionalCI` join `organization` `Organization_org_id` on((`Hypervisor_FunctionalCI`.`org_id` = `Organization_org_id`.`id`))) on((`Hypervisor`.`id` = `Hypervisor_FunctionalCI`.`id`))) where ((0 <> coalesce((`Farm_farm_id_VirtualDevice`.`finalclass` = 'Farm'),1)) and (0 <> coalesce((`Server_server_id_PhysicalDevice`.`finalclass` = 'Server'),1)))
```

