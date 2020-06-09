| 列                                 | 类型                                       | 注释 |
| :--------------------------------- | ------------------------------------------ | ---- |
| id                                 | int [**0**]                                |      |
| name                               | varchar(255) *NULL* []                     |      |
| ipaddress                          | varchar(255) *NULL* []                     |      |
| macaddress                         | varchar(255) *NULL* []                     |      |
| comment                            | text *NULL*                                |      |
| ipgateway                          | varchar(255) *NULL* []                     |      |
| ipmask                             | varchar(255) *NULL* []                     |      |
| speed                              | decimal(12,2) *NULL*                       |      |
| connectableci_id                   | int *NULL* [**0**]                         |      |
| connectableci_name                 | varchar(255) *NULL* []                     |      |
| finalclass                         | varchar(255) *NULL* [**NetworkInterface**] |      |
| friendlyname                       | varchar(511) *NULL*                        |      |
| obsolescence_flag                  | int [**0**]                                |      |
| obsolescence_date                  | date *NULL*                                |      |
| connectableci_id_friendlyname      | varchar(255) *NULL*                        |      |
| connectableci_id_finalclass_recall | varchar(255) *NULL* [**FunctionalCI**]     |      |
| connectableci_id_obsolescence_flag | int [**0**]                                |      |

```
select distinct `PhysicalInterface`.`id` AS `id`,`PhysicalInterface_NetworkInterface`.`name` AS `name`,`PhysicalInterface_IPInterface`.`ipaddress` AS `ipaddress`,`PhysicalInterface_IPInterface`.`macaddress` AS `macaddress`,`PhysicalInterface_IPInterface`.`comment` AS `comment`,`PhysicalInterface_IPInterface`.`ipgateway` AS `ipgateway`,`PhysicalInterface_IPInterface`.`ipmask` AS `ipmask`,`PhysicalInterface_IPInterface`.`speed` AS `speed`,`PhysicalInterface`.`connectableci_id` AS `connectableci_id`,`ConnectableCI_connectableci_id_FunctionalCI`.`name` AS `connectableci_name`,`PhysicalInterface_NetworkInterface`.`finalclass` AS `finalclass`,cast(concat(coalesce(`PhysicalInterface_NetworkInterface`.`name`,''),coalesce(' ',''),coalesce(`ConnectableCI_connectableci_id_FunctionalCI`.`name`,'')) as char charset utf8mb4) AS `friendlyname`,coalesce(coalesce((`ConnectableCI_connectableci_id_PhysicalDevice`.`status` = 'obsolete'),0),0) AS `obsolescence_flag`,`PhysicalInterface_NetworkInterface`.`obsolescence_date` AS `obsolescence_date`,cast(concat(coalesce(`ConnectableCI_connectableci_id_FunctionalCI`.`name`,'')) as char charset utf8mb4) AS `connectableci_id_friendlyname`,`ConnectableCI_connectableci_id_FunctionalCI`.`finalclass` AS `connectableci_id_finalclass_recall`,coalesce((`ConnectableCI_connectableci_id_PhysicalDevice`.`status` = 'obsolete'),0) AS `connectableci_id_obsolescence_flag` from (((`physicalinterface` `PhysicalInterface` join (`physicaldevice` `ConnectableCI_connectableci_id_PhysicalDevice` join `functionalci` `ConnectableCI_connectableci_id_FunctionalCI` on((`ConnectableCI_connectableci_id_PhysicalDevice`.`id` = `ConnectableCI_connectableci_id_FunctionalCI`.`id`))) on((`PhysicalInterface`.`connectableci_id` = `ConnectableCI_connectableci_id_PhysicalDevice`.`id`))) join `ipinterface` `PhysicalInterface_IPInterface` on((`PhysicalInterface`.`id` = `PhysicalInterface_IPInterface`.`id`))) join `networkinterface` `PhysicalInterface_NetworkInterface` on((`PhysicalInterface`.`id` = `PhysicalInterface_NetworkInterface`.`id`))) where (0 <> coalesce((`ConnectableCI_connectableci_id_PhysicalDevice`.`finalclass` in ('DatacenterDevice','NetworkDevice','Server','PC','Printer','StorageSystem','SANSwitch','TapeLibrary','NAS','ConnectableCI')),1))
```

