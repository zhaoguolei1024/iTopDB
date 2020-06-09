| 列                                 | 类型                   | 注释 |
| :--------------------------------- | ---------------------- | ---- |
| id                                 | int [**0**]            |      |
| name                               | varchar(255) *NULL* [] |      |
| lun_id                             | varchar(255) *NULL* [] |      |
| description                        | text *NULL*            |      |
| raid_level                         | varchar(255) *NULL* [] |      |
| size                               | varchar(255) *NULL* [] |      |
| storagesystem_id                   | int *NULL* [**0**]     |      |
| storagesystem_name                 | varchar(255) *NULL* [] |      |
| friendlyname                       | varchar(511) *NULL*    |      |
| obsolescence_flag                  | int [**0**]            |      |
| obsolescence_date                  | date *NULL*            |      |
| storagesystem_id_friendlyname      | varchar(255) *NULL*    |      |
| storagesystem_id_obsolescence_flag | int [**0**]            |      |

```
select distinct `LogicalVolume`.`id` AS `id`,`LogicalVolume`.`name` AS `name`,`LogicalVolume`.`lun_id` AS `lun_id`,`LogicalVolume`.`description` AS `description`,`LogicalVolume`.`raid_level` AS `raid_level`,`LogicalVolume`.`size` AS `size`,`LogicalVolume`.`storagesystem_id` AS `storagesystem_id`,`StorageSystem_storagesystem_id_FunctionalCI`.`name` AS `storagesystem_name`,cast(concat(coalesce(`StorageSystem_storagesystem_id_FunctionalCI`.`name`,''),coalesce(' ',''),coalesce(`LogicalVolume`.`name`,'')) as char charset utf8mb4) AS `friendlyname`,coalesce(coalesce((`StorageSystem_storagesystem_id_PhysicalDevice`.`status` = 'obsolete'),0),0) AS `obsolescence_flag`,`LogicalVolume`.`obsolescence_date` AS `obsolescence_date`,cast(concat(coalesce(`StorageSystem_storagesystem_id_FunctionalCI`.`name`,'')) as char charset utf8mb4) AS `storagesystem_id_friendlyname`,coalesce((`StorageSystem_storagesystem_id_PhysicalDevice`.`status` = 'obsolete'),0) AS `storagesystem_id_obsolescence_flag` from (`logicalvolume` `LogicalVolume` join (`physicaldevice` `StorageSystem_storagesystem_id_PhysicalDevice` join `functionalci` `StorageSystem_storagesystem_id_FunctionalCI` on((`StorageSystem_storagesystem_id_PhysicalDevice`.`id` = `StorageSystem_storagesystem_id_FunctionalCI`.`id`))) on((`LogicalVolume`.`storagesystem_id` = `StorageSystem_storagesystem_id_PhysicalDevice`.`id`))) where (0 <> coalesce((`StorageSystem_storagesystem_id_PhysicalDevice`.`finalclass` = 'StorageSystem'),1))
```

