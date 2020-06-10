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
SELECT DISTINCT
	`NASFileSystem`.`id` AS `id`,
	`NASFileSystem`.`name` AS `name`,
	`NASFileSystem`.`description` AS `description`,
	`NASFileSystem`.`raid_level` AS `raid_level`,
	`NASFileSystem`.`size` AS `size`,
	`NASFileSystem`.`nas_id` AS `nas_id`,
	`NAS_nas_id_FunctionalCI`.`name` AS `nas_name`,
	cast( concat( COALESCE ( `NASFileSystem`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `friendlyname`,
	COALESCE ( COALESCE (( `NAS_nas_id_PhysicalDevice`.`status` = 'obsolete' ), 0 ), 0 ) AS `obsolescence_flag`,
	`NASFileSystem`.`obsolescence_date` AS `obsolescence_date`,
	cast( concat( COALESCE ( `NAS_nas_id_FunctionalCI`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `nas_id_friendlyname`,
	COALESCE (( `NAS_nas_id_PhysicalDevice`.`status` = 'obsolete' ), 0 ) AS `nas_id_obsolescence_flag` 
FROM
	(
		`nasfilesystem` `NASFileSystem`
		JOIN (
			`physicaldevice` `NAS_nas_id_PhysicalDevice`
			JOIN `functionalci` `NAS_nas_id_FunctionalCI` ON ((
					`NAS_nas_id_PhysicalDevice`.`id` = `NAS_nas_id_FunctionalCI`.`id` 
					))) ON ((
				`NASFileSystem`.`nas_id` = `NAS_nas_id_PhysicalDevice`.`id` 
			))) 
WHERE
	(
	0 <> COALESCE (( `NAS_nas_id_PhysicalDevice`.`finalclass` = 'NAS' ), 1 ))
```

