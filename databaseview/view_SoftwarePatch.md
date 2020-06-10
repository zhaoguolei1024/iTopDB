| 列                       | 类型                            | 注释 |
| :----------------------- | ------------------------------- | ---- |
| id                       | int [**0**]                     |      |
| name                     | varchar(255) *NULL* []          |      |
| description              | text *NULL*                     |      |
| software_id              | int *NULL* [**0**]              |      |
| software_name            | varchar(255) *NULL* []          |      |
| finalclass               | varchar(255) *NULL* [**Patch**] |      |
| friendlyname             | varchar(255) *NULL*             |      |
| software_id_friendlyname | varchar(511) *NULL*             |      |

```
SELECT DISTINCT
	`SoftwarePatch`.`id` AS `id`,
	`SoftwarePatch_Patch`.`name` AS `name`,
	`SoftwarePatch_Patch`.`description` AS `description`,
	`SoftwarePatch`.`software_id` AS `software_id`,
	`Software_software_id`.`name` AS `software_name`,
	`SoftwarePatch_Patch`.`finalclass` AS `finalclass`,
	cast( concat( COALESCE ( `SoftwarePatch_Patch`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `friendlyname`,
	cast(
		concat(
			COALESCE ( `Software_software_id`.`name`, '' ),
			COALESCE ( ' ', '' ),
		COALESCE ( `Software_software_id`.`version`, '' )) AS CHAR charset utf8mb4 
	) AS `software_id_friendlyname` 
FROM
	((
			`softwarepatch` `SoftwarePatch`
			JOIN `software` `Software_software_id` ON ((
					`SoftwarePatch`.`software_id` = `Software_software_id`.`id` 
				)))
		JOIN `patch` `SoftwarePatch_Patch` ON ((
				`SoftwarePatch`.`id` = `SoftwarePatch_Patch`.`id` 
			))) 
WHERE
	(
	0 <> 1)
```

