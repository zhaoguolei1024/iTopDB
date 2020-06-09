| 列                               | 类型                   | 注释 |
| :------------------------------- | ---------------------- | ---- |
| id                               | int [**0**]            |      |
| name                             | varchar(255) *NULL* [] |      |
| description                      | text *NULL*            |      |
| size                             | varchar(255) *NULL* [] |      |
| tapelibrary_id                   | int *NULL* [**0**]     |      |
| tapelibrary_name                 | varchar(255) *NULL* [] |      |
| friendlyname                     | varchar(255) *NULL*    |      |
| obsolescence_flag                | int [**0**]            |      |
| obsolescence_date                | date *NULL*            |      |
| tapelibrary_id_friendlyname      | varchar(255) *NULL*    |      |
| tapelibrary_id_obsolescence_flag | int [**0**]            |      |

```
select distinct `Tape`.`id` AS `id`,`Tape`.`name` AS `name`,`Tape`.`description` AS `description`,`Tape`.`size` AS `size`,`Tape`.`tapelibrary_id` AS `tapelibrary_id`,`TapeLibrary_tapelibrary_id_FunctionalCI`.`name` AS `tapelibrary_name`,cast(concat(coalesce(`Tape`.`name`,'')) as char charset utf8mb4) AS `friendlyname`,coalesce(coalesce((`TapeLibrary_tapelibrary_id_PhysicalDevice`.`status` = 'obsolete'),0),0) AS `obsolescence_flag`,`Tape`.`obsolescence_date` AS `obsolescence_date`,cast(concat(coalesce(`TapeLibrary_tapelibrary_id_FunctionalCI`.`name`,'')) as char charset utf8mb4) AS `tapelibrary_id_friendlyname`,coalesce((`TapeLibrary_tapelibrary_id_PhysicalDevice`.`status` = 'obsolete'),0) AS `tapelibrary_id_obsolescence_flag` from (`tape` `Tape` join (`physicaldevice` `TapeLibrary_tapelibrary_id_PhysicalDevice` join `functionalci` `TapeLibrary_tapelibrary_id_FunctionalCI` on((`TapeLibrary_tapelibrary_id_PhysicalDevice`.`id` = `TapeLibrary_tapelibrary_id_FunctionalCI`.`id`))) on((`Tape`.`tapelibrary_id` = `TapeLibrary_tapelibrary_id_PhysicalDevice`.`id`))) where (0 <> coalesce((`TapeLibrary_tapelibrary_id_PhysicalDevice`.`finalclass` = 'TapeLibrary'),1))
```

