| 列                                    | 类型                                   | 注释 |
| :------------------------------------ | -------------------------------------- | ---- |
| id                                    | int [**0**]                            |      |
| softwarepatch_id                      | int *NULL* [**0**]                     |      |
| softwarepatch_name                    | varchar(255) *NULL* []                 |      |
| softwareinstance_id                   | int *NULL* [**0**]                     |      |
| softwareinstance_name                 | varchar(255) *NULL* []                 |      |
| friendlyname                          | varchar(23) *NULL*                     |      |
| softwarepatch_id_friendlyname         | varchar(255) *NULL*                    |      |
| softwareinstance_id_friendlyname      | varchar(511) *NULL*                    |      |
| softwareinstance_id_finalclass_recall | varchar(255) *NULL* [**FunctionalCI**] |      |
| softwareinstance_id_obsolescence_flag | int [**0**]                            |      |

```
select distinct `lnkSoftwareInstanceToSoftwarePatch`.`id` AS `id`,`lnkSoftwareInstanceToSoftwarePatch`.`softwarepatch_id` AS `softwarepatch_id`,`SoftwarePatch_softwarepatch_id_Patch`.`name` AS `softwarepatch_name`,`lnkSoftwareInstanceToSoftwarePatch`.`softwareinstance_id` AS `softwareinstance_id`,`SoftwareInstance_softwareinstance_id_FunctionalCI`.`name` AS `softwareinstance_name`,cast(concat(coalesce(`lnkSoftwareInstanceToSoftwarePatch`.`softwarepatch_id`,''),coalesce(' ',''),coalesce(`lnkSoftwareInstanceToSoftwarePatch`.`softwareinstance_id`,'')) as char charset utf8mb4) AS `friendlyname`,cast(concat(coalesce(`SoftwarePatch_softwarepatch_id_Patch`.`name`,'')) as char charset utf8mb4) AS `softwarepatch_id_friendlyname`,cast(concat(coalesce(`SoftwareInstance_softwareinstance_id_FunctionalCI`.`name`,''),coalesce(' ',''),coalesce(`FunctionalCI_system_id`.`name`,'')) as char charset utf8mb4) AS `softwareinstance_id_friendlyname`,`SoftwareInstance_softwareinstance_id_FunctionalCI`.`finalclass` AS `softwareinstance_id_finalclass_recall`,coalesce((`SoftwareInstance_softwareinstance_id`.`status` = 'inactive'),0) AS `softwareinstance_id_obsolescence_flag` from ((`lnksoftwareinstancetosoftwarepatch` `lnkSoftwareInstanceToSoftwarePatch` join `patch` `SoftwarePatch_softwarepatch_id_Patch` on((`lnkSoftwareInstanceToSoftwarePatch`.`softwarepatch_id` = `SoftwarePatch_softwarepatch_id_Patch`.`id`))) join ((`softwareinstance` `SoftwareInstance_softwareinstance_id` join `functionalci` `FunctionalCI_system_id` on((`SoftwareInstance_softwareinstance_id`.`functionalci_id` = `FunctionalCI_system_id`.`id`))) join `functionalci` `SoftwareInstance_softwareinstance_id_FunctionalCI` on((`SoftwareInstance_softwareinstance_id`.`id` = `SoftwareInstance_softwareinstance_id_FunctionalCI`.`id`))) on((`lnkSoftwareInstanceToSoftwarePatch`.`softwareinstance_id` = `SoftwareInstance_softwareinstance_id`.`id`))) where (0 <> coalesce((`SoftwarePatch_softwarepatch_id_Patch`.`finalclass` = 'SoftwarePatch'),1))
```

