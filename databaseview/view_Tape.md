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
SELECT DISTINCT
	`Tape`.`id` AS `id`,
	`Tape`.`name` AS `name`,
	`Tape`.`description` AS `description`,
	`Tape`.`size` AS `size`,
	`Tape`.`tapelibrary_id` AS `tapelibrary_id`,
	`TapeLibrary_tapelibrary_id_FunctionalCI`.`name` AS `tapelibrary_name`,
	cast( concat( COALESCE ( `Tape`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `friendlyname`,
	COALESCE ( COALESCE (( `TapeLibrary_tapelibrary_id_PhysicalDevice`.`status` = 'obsolete' ), 0 ), 0 ) AS `obsolescence_flag`,
	`Tape`.`obsolescence_date` AS `obsolescence_date`,
	cast( concat( COALESCE ( `TapeLibrary_tapelibrary_id_FunctionalCI`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `tapelibrary_id_friendlyname`,
	COALESCE (( `TapeLibrary_tapelibrary_id_PhysicalDevice`.`status` = 'obsolete' ), 0 ) AS `tapelibrary_id_obsolescence_flag` 
FROM
	(
		`tape` `Tape`
		JOIN (
			`physicaldevice` `TapeLibrary_tapelibrary_id_PhysicalDevice`
			JOIN `functionalci` `TapeLibrary_tapelibrary_id_FunctionalCI` ON ((
					`TapeLibrary_tapelibrary_id_PhysicalDevice`.`id` = `TapeLibrary_tapelibrary_id_FunctionalCI`.`id` 
					))) ON ((
				`Tape`.`tapelibrary_id` = `TapeLibrary_tapelibrary_id_PhysicalDevice`.`id` 
			))) 
WHERE
	(
	0 <> COALESCE (( `TapeLibrary_tapelibrary_id_PhysicalDevice`.`finalclass` = 'TapeLibrary' ), 1 ))
```

