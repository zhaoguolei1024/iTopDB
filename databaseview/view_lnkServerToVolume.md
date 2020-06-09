| 列                          | 类型                   | 注释 |
| :-------------------------- | ---------------------- | ---- |
| id                          | int [**0**]            |      |
| volume_id                   | int *NULL* [**0**]     |      |
| volume_name                 | varchar(255) *NULL* [] |      |
| server_id                   | int *NULL* [**0**]     |      |
| server_name                 | varchar(255) *NULL* [] |      |
| size_used                   | varchar(255) *NULL* [] |      |
| friendlyname                | varchar(11) *NULL*     |      |
| volume_id_friendlyname      | varchar(511) *NULL*    |      |
| volume_id_obsolescence_flag | int [**0**]            |      |
| server_id_friendlyname      | varchar(255) *NULL*    |      |
| server_id_obsolescence_flag | int [**0**]            |      |

```
select distinct `lnkServerToVolume`.`id` AS `id`,`lnkServerToVolume`.`volume_id` AS `volume_id`,`LogicalVolume_volume_id`.`name` AS `volume_name`,`lnkServerToVolume`.`server_id` AS `server_id`,`Server_server_id_FunctionalCI`.`name` AS `server_name`,`lnkServerToVolume`.`size_used` AS `size_used`,cast(concat(coalesce(`lnkServerToVolume`.`volume_id`,'')) as char charset utf8mb4) AS `friendlyname`,cast(concat(coalesce(`StorageSystem_storagesystem_id_FunctionalCI`.`name`,''),coalesce(' ',''),coalesce(`LogicalVolume_volume_id`.`name`,'')) as char charset utf8mb4) AS `volume_id_friendlyname`,coalesce(coalesce((`StorageSystem_storagesystem_id_PhysicalDevice`.`status` = 'obsolete'),0),0) AS `volume_id_obsolescence_flag`,cast(concat(coalesce(`Server_server_id_FunctionalCI`.`name`,'')) as char charset utf8mb4) AS `server_id_friendlyname`,coalesce((`Server_server_id_PhysicalDevice`.`status` = 'obsolete'),0) AS `server_id_obsolescence_flag` from ((`lnkservertovolume` `lnkServerToVolume` join (`logicalvolume` `LogicalVolume_volume_id` join (`physicaldevice` `StorageSystem_storagesystem_id_PhysicalDevice` join `functionalci` `StorageSystem_storagesystem_id_FunctionalCI` on((`StorageSystem_storagesystem_id_PhysicalDevice`.`id` = `StorageSystem_storagesystem_id_FunctionalCI`.`id`))) on((`LogicalVolume_volume_id`.`storagesystem_id` = `StorageSystem_storagesystem_id_PhysicalDevice`.`id`))) on((`lnkServerToVolume`.`volume_id` = `LogicalVolume_volume_id`.`id`))) join (`physicaldevice` `Server_server_id_PhysicalDevice` join `functionalci` `Server_server_id_FunctionalCI` on((`Server_server_id_PhysicalDevice`.`id` = `Server_server_id_FunctionalCI`.`id`))) on((`lnkServerToVolume`.`server_id` = `Server_server_id_PhysicalDevice`.`id`))) where ((0 <> coalesce((`StorageSystem_storagesystem_id_PhysicalDevice`.`finalclass` = 'StorageSystem'),1)) and (0 <> coalesce((`Server_server_id_PhysicalDevice`.`finalclass` = 'Server'),1)))
```

