| 列                       | 类型                   | 注释 |
| :----------------------- | ---------------------- | ---- |
| id                       | int [**0**]            |      |
| name                     | varchar(255) *NULL* [] |      |
| description              | text *NULL*            |      |
| raid_level               | varchar(255) *NULL* [] |      |
| size                     | varchar(255) *NULL* [] |      |
| nas_id                   | int *NULL* [**0**]     |      |
| nas_name                 | varchar(255) *NULL* [] |      |
| friendlyname             | varchar(255) *NULL*    |      |
| obsolescence_flag        | int [**0**]            |      |
| obsolescence_date        | date *NULL*            |      |
| nas_id_friendlyname      | varchar(255) *NULL*    |      |
| nas_id_obsolescence_flag | int [**0**]            |      |

```
select distinct `NASFileSystem`.`id` AS `id`,`NASFileSystem`.`name` AS `name`,`NASFileSystem`.`description` AS `description`,`NASFileSystem`.`raid_level` AS `raid_level`,`NASFileSystem`.`size` AS `size`,`NASFileSystem`.`nas_id` AS `nas_id`,`NAS_nas_id_FunctionalCI`.`name` AS `nas_name`,cast(concat(coalesce(`NASFileSystem`.`name`,'')) as char charset utf8mb4) AS `friendlyname`,coalesce(coalesce((`NAS_nas_id_PhysicalDevice`.`status` = 'obsolete'),0),0) AS `obsolescence_flag`,`NASFileSystem`.`obsolescence_date` AS `obsolescence_date`,cast(concat(coalesce(`NAS_nas_id_FunctionalCI`.`name`,'')) as char charset utf8mb4) AS `nas_id_friendlyname`,coalesce((`NAS_nas_id_PhysicalDevice`.`status` = 'obsolete'),0) AS `nas_id_obsolescence_flag` from (`nasfilesystem` `NASFileSystem` join (`physicaldevice` `NAS_nas_id_PhysicalDevice` join `functionalci` `NAS_nas_id_FunctionalCI` on((`NAS_nas_id_PhysicalDevice`.`id` = `NAS_nas_id_FunctionalCI`.`id`))) on((`NASFileSystem`.`nas_id` = `NAS_nas_id_PhysicalDevice`.`id`))) where (0 <> coalesce((`NAS_nas_id_PhysicalDevice`.`finalclass` = 'NAS'),1))
```

