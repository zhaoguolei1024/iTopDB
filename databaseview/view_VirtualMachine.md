| 列                               | 类型                                                         | 注释 |
| :------------------------------- | ------------------------------------------------------------ | ---- |
| id                               | int [**0**]                                                  |      |
| name                             | varchar(255) *NULL* []                                       |      |
| description                      | text *NULL*                                                  |      |
| org_id                           | int *NULL* [**0**]                                           |      |
| organization_name                | varchar(255) *NULL* []                                       |      |
| business_criticity               | enum('high','low','medium') *NULL* [**low**]                 |      |
| move2production                  | date *NULL*                                                  |      |
| status                           | enum('implementation','obsolete','production','stock') *NULL* [**production**] |      |
| virtualhost_id                   | int *NULL* [**0**]                                           |      |
| virtualhost_name                 | varchar(255) *NULL* []                                       |      |
| osfamily_id                      | int *NULL* [**0**]                                           |      |
| osfamily_name                    | varchar(255) *NULL* []                                       |      |
| osversion_id                     | int *NULL* [**0**]                                           |      |
| osversion_name                   | varchar(255) *NULL* []                                       |      |
| oslicence_id                     | int *NULL* [**0**]                                           |      |
| oslicence_name                   | varchar(255) *NULL* []                                       |      |
| cpu                              | varchar(255) *NULL* []                                       |      |
| ram                              | varchar(255) *NULL* []                                       |      |
| managementip                     | varchar(255) *NULL* []                                       |      |
| finalclass                       | varchar(255) *NULL* [**FunctionalCI**]                       |      |
| friendlyname                     | varchar(255) *NULL*                                          |      |
| obsolescence_flag                | int [**0**]                                                  |      |
| obsolescence_date                | date *NULL*                                                  |      |
| org_id_friendlyname              | varchar(255) *NULL*                                          |      |
| org_id_obsolescence_flag         | int [**0**]                                                  |      |
| virtualhost_id_friendlyname      | varchar(255) *NULL*                                          |      |
| virtualhost_id_finalclass_recall | varchar(255) *NULL* [**FunctionalCI**]                       |      |
| virtualhost_id_obsolescence_flag | int [**0**]                                                  |      |
| osfamily_id_friendlyname         | varchar(255) *NULL*                                          |      |
| osversion_id_friendlyname        | varchar(255) *NULL*                                          |      |
| oslicence_id_friendlyname        | varchar(255) *NULL*                                          |      |
| oslicence_id_obsolescence_flag   | int [**0**]                                                  |      |

```
select distinct `VirtualMachine`.`id` AS `id`,`VirtualMachine_FunctionalCI`.`name` AS `name`,`VirtualMachine_FunctionalCI`.`description` AS `description`,`VirtualMachine_FunctionalCI`.`org_id` AS `org_id`,`Organization_org_id`.`name` AS `organization_name`,`VirtualMachine_FunctionalCI`.`business_criticity` AS `business_criticity`,`VirtualMachine_FunctionalCI`.`move2production` AS `move2production`,`VirtualMachine_VirtualDevice`.`status` AS `status`,`VirtualMachine`.`virtualhost_id` AS `virtualhost_id`,`VirtualHost_virtualhost_id_FunctionalCI`.`name` AS `virtualhost_name`,`VirtualMachine`.`osfamily_id` AS `osfamily_id`,`OSFamily_osfamily_id_Typology`.`name` AS `osfamily_name`,`VirtualMachine`.`osversion_id` AS `osversion_id`,`OSVersion_osversion_id_Typology`.`name` AS `osversion_name`,`VirtualMachine`.`oslicence_id` AS `oslicence_id`,`OSLicence_oslicence_id_Licence`.`name` AS `oslicence_name`,`VirtualMachine`.`cpu` AS `cpu`,`VirtualMachine`.`ram` AS `ram`,`VirtualMachine`.`managementip` AS `managementip`,`VirtualMachine_FunctionalCI`.`finalclass` AS `finalclass`,cast(concat(coalesce(`VirtualMachine_FunctionalCI`.`name`,'')) as char charset utf8mb4) AS `friendlyname`,coalesce((`VirtualMachine_VirtualDevice`.`status` = 'obsolete'),0) AS `obsolescence_flag`,`VirtualMachine_FunctionalCI`.`obsolescence_date` AS `obsolescence_date`,cast(concat(coalesce(`Organization_org_id`.`name`,'')) as char charset utf8mb4) AS `org_id_friendlyname`,coalesce((`Organization_org_id`.`status` = 'inactive'),0) AS `org_id_obsolescence_flag`,cast(concat(coalesce(`VirtualHost_virtualhost_id_FunctionalCI`.`name`,'')) as char charset utf8mb4) AS `virtualhost_id_friendlyname`,`VirtualHost_virtualhost_id_FunctionalCI`.`finalclass` AS `virtualhost_id_finalclass_recall`,coalesce((`VirtualHost_virtualhost_id_VirtualDevice`.`status` = 'obsolete'),0) AS `virtualhost_id_obsolescence_flag`,cast(concat(coalesce(`OSFamily_osfamily_id_Typology`.`name`,'')) as char charset utf8mb4) AS `osfamily_id_friendlyname`,cast(concat(coalesce(`OSVersion_osversion_id_Typology`.`name`,'')) as char charset utf8mb4) AS `osversion_id_friendlyname`,cast(concat(coalesce(`OSLicence_oslicence_id_Licence`.`name`,'')) as char charset utf8mb4) AS `oslicence_id_friendlyname`,coalesce(((`OSLicence_oslicence_id_Licence`.`perpetual` = 'no') and ((`OSLicence_oslicence_id_Licence`.`end_date` is null) = 0) and (`OSLicence_oslicence_id_Licence`.`end_date` < date_format((now() - interval 15 month),'%Y-%m-%d 00:00:00'))),0) AS `oslicence_id_obsolescence_flag` from ((((((`virtualmachine` `VirtualMachine` join (`virtualdevice` `VirtualHost_virtualhost_id_VirtualDevice` join `functionalci` `VirtualHost_virtualhost_id_FunctionalCI` on((`VirtualHost_virtualhost_id_VirtualDevice`.`id` = `VirtualHost_virtualhost_id_FunctionalCI`.`id`))) on((`VirtualMachine`.`virtualhost_id` = `VirtualHost_virtualhost_id_VirtualDevice`.`id`))) left join `typology` `OSFamily_osfamily_id_Typology` on((`VirtualMachine`.`osfamily_id` = `OSFamily_osfamily_id_Typology`.`id`))) left join `typology` `OSVersion_osversion_id_Typology` on((`VirtualMachine`.`osversion_id` = `OSVersion_osversion_id_Typology`.`id`))) left join `licence` `OSLicence_oslicence_id_Licence` on((`VirtualMachine`.`oslicence_id` = `OSLicence_oslicence_id_Licence`.`id`))) join `virtualdevice` `VirtualMachine_VirtualDevice` on((`VirtualMachine`.`id` = `VirtualMachine_VirtualDevice`.`id`))) join (`functionalci` `VirtualMachine_FunctionalCI` join `organization` `Organization_org_id` on((`VirtualMachine_FunctionalCI`.`org_id` = `Organization_org_id`.`id`))) on((`VirtualMachine`.`id` = `VirtualMachine_FunctionalCI`.`id`))) where ((0 <> coalesce((`VirtualHost_virtualhost_id_VirtualDevice`.`finalclass` in ('Hypervisor','Farm','VirtualHost')),1)) and (0 <> coalesce((`OSFamily_osfamily_id_Typology`.`finalclass` = 'OSFamily'),1)) and (0 <> coalesce((`OSVersion_osversion_id_Typology`.`finalclass` = 'OSVersion'),1)) and (0 <> coalesce((`OSLicence_oslicence_id_Licence`.`finalclass` = 'OSLicence'),1)))
```

