| 列                                    | 类型                                       | 注释 |
| :------------------------------------ | ------------------------------------------ | ---- |
| id                                    | int [**0**]                                |      |
| name                                  | varchar(255) *NULL* []                     |      |
| speed                                 | decimal(6,2) *NULL*                        |      |
| topology                              | varchar(255) *NULL* []                     |      |
| wwn                                   | varchar(255) *NULL* []                     |      |
| datacenterdevice_id                   | int *NULL* [**0**]                         |      |
| datacenterdevice_name                 | varchar(255) *NULL* []                     |      |
| finalclass                            | varchar(255) *NULL* [**NetworkInterface**] |      |
| friendlyname                          | varchar(511) *NULL*                        |      |
| obsolescence_flag                     | int [**0**]                                |      |
| obsolescence_date                     | date *NULL*                                |      |
| datacenterdevice_id_friendlyname      | varchar(255) *NULL*                        |      |
| datacenterdevice_id_finalclass_recall | varchar(255) *NULL* [**FunctionalCI**]     |      |
| datacenterdevice_id_obsolescence_flag | int [**0**]                                |      |

```
select distinct `FiberChannelInterface`.`id` AS `id`,`FiberChannelInterface_NetworkInterface`.`name` AS `name`,`FiberChannelInterface`.`speed` AS `speed`,`FiberChannelInterface`.`topology` AS `topology`,`FiberChannelInterface`.`wwn` AS `wwn`,`FiberChannelInterface`.`datacenterdevice_id` AS `datacenterdevice_id`,`DatacenterDevice_datacenterdevice_id_FunctionalCI`.`name` AS `datacenterdevice_name`,`FiberChannelInterface_NetworkInterface`.`finalclass` AS `finalclass`,cast(concat(coalesce(`FiberChannelInterface_NetworkInterface`.`name`,''),coalesce(' ',''),coalesce(`DatacenterDevice_datacenterdevice_id_FunctionalCI`.`name`,'')) as char charset utf8mb4) AS `friendlyname`,coalesce(coalesce((`DatacenterDevice_datacenterdevice_id_PhysicalDevice`.`status` = 'obsolete'),0),0) AS `obsolescence_flag`,`FiberChannelInterface_NetworkInterface`.`obsolescence_date` AS `obsolescence_date`,cast(concat(coalesce(`DatacenterDevice_datacenterdevice_id_FunctionalCI`.`name`,'')) as char charset utf8mb4) AS `datacenterdevice_id_friendlyname`,`DatacenterDevice_datacenterdevice_id_FunctionalCI`.`finalclass` AS `datacenterdevice_id_finalclass_recall`,coalesce((`DatacenterDevice_datacenterdevice_id_PhysicalDevice`.`status` = 'obsolete'),0) AS `datacenterdevice_id_obsolescence_flag` from ((`fiberchannelinterface` `FiberChannelInterface` join (`physicaldevice` `DatacenterDevice_datacenterdevice_id_PhysicalDevice` join `functionalci` `DatacenterDevice_datacenterdevice_id_FunctionalCI` on((`DatacenterDevice_datacenterdevice_id_PhysicalDevice`.`id` = `DatacenterDevice_datacenterdevice_id_FunctionalCI`.`id`))) on((`FiberChannelInterface`.`datacenterdevice_id` = `DatacenterDevice_datacenterdevice_id_PhysicalDevice`.`id`))) join `networkinterface` `FiberChannelInterface_NetworkInterface` on((`FiberChannelInterface`.`id` = `FiberChannelInterface_NetworkInterface`.`id`))) where (0 <> coalesce((`DatacenterDevice_datacenterdevice_id_PhysicalDevice`.`finalclass` in ('NetworkDevice','Server','StorageSystem','SANSwitch','TapeLibrary','NAS','DatacenterDevice')),1))
```

