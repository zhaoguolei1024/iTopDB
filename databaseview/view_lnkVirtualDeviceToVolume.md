| 列                                 | 类型                                   | 注释 |
| :--------------------------------- | -------------------------------------- | ---- |
| id                                 | int [**0**]                            |      |
| volume_id                          | int *NULL* [**0**]                     |      |
| volume_name                        | varchar(255) *NULL* []                 |      |
| virtualdevice_id                   | int *NULL* [**0**]                     |      |
| virtualdevice_name                 | varchar(255) *NULL* []                 |      |
| size_used                          | varchar(255) *NULL* []                 |      |
| friendlyname                       | varchar(11) *NULL*                     |      |
| volume_id_friendlyname             | varchar(511) *NULL*                    |      |
| volume_id_obsolescence_flag        | int [**0**]                            |      |
| virtualdevice_id_friendlyname      | varchar(255) *NULL*                    |      |
| virtualdevice_id_finalclass_recall | varchar(255) *NULL* [**FunctionalCI**] |      |
| virtualdevice_id_obsolescence_flag | int [**0**]                            |      |

```
select distinct `lnkVirtualDeviceToVolume`.`id` AS `id`,`lnkVirtualDeviceToVolume`.`volume_id` AS `volume_id`,`LogicalVolume_volume_id`.`name` AS `volume_name`,`lnkVirtualDeviceToVolume`.`virtualdevice_id` AS `virtualdevice_id`,`VirtualDevice_virtualdevice_id_FunctionalCI`.`name` AS `virtualdevice_name`,`lnkVirtualDeviceToVolume`.`size_used` AS `size_used`,cast(concat(coalesce(`lnkVirtualDeviceToVolume`.`volume_id`,'')) as char charset utf8mb4) AS `friendlyname`,cast(concat(coalesce(`StorageSystem_storagesystem_id_FunctionalCI`.`name`,''),coalesce(' ',''),coalesce(`LogicalVolume_volume_id`.`name`,'')) as char charset utf8mb4) AS `volume_id_friendlyname`,coalesce(coalesce((`StorageSystem_storagesystem_id_PhysicalDevice`.`status` = 'obsolete'),0),0) AS `volume_id_obsolescence_flag`,cast(concat(coalesce(`VirtualDevice_virtualdevice_id_FunctionalCI`.`name`,'')) as char charset utf8mb4) AS `virtualdevice_id_friendlyname`,`VirtualDevice_virtualdevice_id_FunctionalCI`.`finalclass` AS `virtualdevice_id_finalclass_recall`,coalesce((`VirtualDevice_virtualdevice_id`.`status` = 'obsolete'),0) AS `virtualdevice_id_obsolescence_flag` from ((`lnkvirtualdevicetovolume` `lnkVirtualDeviceToVolume` join (`logicalvolume` `LogicalVolume_volume_id` join (`physicaldevice` `StorageSystem_storagesystem_id_PhysicalDevice` join `functionalci` `StorageSystem_storagesystem_id_FunctionalCI` on((`StorageSystem_storagesystem_id_PhysicalDevice`.`id` = `StorageSystem_storagesystem_id_FunctionalCI`.`id`))) on((`LogicalVolume_volume_id`.`storagesystem_id` = `StorageSystem_storagesystem_id_PhysicalDevice`.`id`))) on((`lnkVirtualDeviceToVolume`.`volume_id` = `LogicalVolume_volume_id`.`id`))) join (`virtualdevice` `VirtualDevice_virtualdevice_id` join `functionalci` `VirtualDevice_virtualdevice_id_FunctionalCI` on((`VirtualDevice_virtualdevice_id`.`id` = `VirtualDevice_virtualdevice_id_FunctionalCI`.`id`))) on((`lnkVirtualDeviceToVolume`.`virtualdevice_id` = `VirtualDevice_virtualdevice_id`.`id`))) where (0 <> coalesce((`StorageSystem_storagesystem_id_PhysicalDevice`.`finalclass` = 'StorageSystem'),1))
```

