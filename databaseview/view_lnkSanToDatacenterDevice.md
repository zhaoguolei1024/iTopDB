| 列                                    | 类型                                   | 注释 |
| :------------------------------------ | -------------------------------------- | ---- |
| id                                    | int [**0**]                            |      |
| san_id                                | int *NULL* [**0**]                     |      |
| san_name                              | varchar(255) *NULL* []                 |      |
| datacenterdevice_id                   | int *NULL* [**0**]                     |      |
| datacenterdevice_name                 | varchar(255) *NULL* []                 |      |
| san_port                              | varchar(255) *NULL* []                 |      |
| datacenterdevice_port                 | varchar(255) *NULL* []                 |      |
| friendlyname                          | varchar(11) *NULL*                     |      |
| san_id_friendlyname                   | varchar(255) *NULL*                    |      |
| san_id_obsolescence_flag              | int [**0**]                            |      |
| datacenterdevice_id_friendlyname      | varchar(255) *NULL*                    |      |
| datacenterdevice_id_finalclass_recall | varchar(255) *NULL* [**FunctionalCI**] |      |
| datacenterdevice_id_obsolescence_flag | int [**0**]                            |      |

```
select distinct `lnkSanToDatacenterDevice`.`id` AS `id`,`lnkSanToDatacenterDevice`.`san_id` AS `san_id`,`SANSwitch_san_id_FunctionalCI`.`name` AS `san_name`,`lnkSanToDatacenterDevice`.`datacenterdevice_id` AS `datacenterdevice_id`,`DatacenterDevice_datacenterdevice_id_FunctionalCI`.`name` AS `datacenterdevice_name`,`lnkSanToDatacenterDevice`.`san_port` AS `san_port`,`lnkSanToDatacenterDevice`.`datacenterdevice_port` AS `datacenterdevice_port`,cast(concat(coalesce(`lnkSanToDatacenterDevice`.`san_id`,'')) as char charset utf8mb4) AS `friendlyname`,cast(concat(coalesce(`SANSwitch_san_id_FunctionalCI`.`name`,'')) as char charset utf8mb4) AS `san_id_friendlyname`,coalesce((`SANSwitch_san_id_PhysicalDevice`.`status` = 'obsolete'),0) AS `san_id_obsolescence_flag`,cast(concat(coalesce(`DatacenterDevice_datacenterdevice_id_FunctionalCI`.`name`,'')) as char charset utf8mb4) AS `datacenterdevice_id_friendlyname`,`DatacenterDevice_datacenterdevice_id_FunctionalCI`.`finalclass` AS `datacenterdevice_id_finalclass_recall`,coalesce((`DatacenterDevice_datacenterdevice_id_PhysicalDevice`.`status` = 'obsolete'),0) AS `datacenterdevice_id_obsolescence_flag` from ((`lnkdatacenterdevicetosan` `lnkSanToDatacenterDevice` join (`physicaldevice` `SANSwitch_san_id_PhysicalDevice` join `functionalci` `SANSwitch_san_id_FunctionalCI` on((`SANSwitch_san_id_PhysicalDevice`.`id` = `SANSwitch_san_id_FunctionalCI`.`id`))) on((`lnkSanToDatacenterDevice`.`san_id` = `SANSwitch_san_id_PhysicalDevice`.`id`))) join (`physicaldevice` `DatacenterDevice_datacenterdevice_id_PhysicalDevice` join `functionalci` `DatacenterDevice_datacenterdevice_id_FunctionalCI` on((`DatacenterDevice_datacenterdevice_id_PhysicalDevice`.`id` = `DatacenterDevice_datacenterdevice_id_FunctionalCI`.`id`))) on((`lnkSanToDatacenterDevice`.`datacenterdevice_id` = `DatacenterDevice_datacenterdevice_id_PhysicalDevice`.`id`))) where ((0 <> coalesce((`SANSwitch_san_id_PhysicalDevice`.`finalclass` = 'SANSwitch'),1)) and (0 <> coalesce((`DatacenterDevice_datacenterdevice_id_PhysicalDevice`.`finalclass` in ('NetworkDevice','Server','StorageSystem','SANSwitch','TapeLibrary','NAS','DatacenterDevice')),1)))
```

