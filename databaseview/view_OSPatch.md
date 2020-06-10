| 列                        | 类型                            | 注释 |
| :------------------------ | ------------------------------- | ---- |
| id                        | int [**0**]                     |      |
| name                      | varchar(255) *NULL* []          |      |
| description               | text *NULL*                     |      |
| osversion_id              | int *NULL* [**0**]              |      |
| osversion_name            | varchar(255) *NULL* []          |      |
| finalclass                | varchar(255) *NULL* [**Patch**] |      |
| friendlyname              | varchar(255) *NULL*             |      |
| osversion_id_friendlyname | varchar(255) *NULL*             |      |

```
SELECT DISTINCT
	`OSPatch`.`id` AS `id`,
	`OSPatch_Patch`.`name` AS `name`,
	`OSPatch_Patch`.`description` AS `description`,
	`OSPatch`.`osversion_id` AS `osversion_id`,
	`OSVersion_osversion_id_Typology`.`name` AS `osversion_name`,
	`OSPatch_Patch`.`finalclass` AS `finalclass`,
	cast( concat( COALESCE ( `OSPatch_Patch`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `friendlyname`,
	cast( concat( COALESCE ( `OSVersion_osversion_id_Typology`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `osversion_id_friendlyname` 
FROM
	((
			`ospatch` `OSPatch`
			JOIN `typology` `OSVersion_osversion_id_Typology` ON ((
					`OSPatch`.`osversion_id` = `OSVersion_osversion_id_Typology`.`id` 
				)))
		JOIN `patch` `OSPatch_Patch` ON ((
				`OSPatch`.`id` = `OSPatch_Patch`.`id` 
			))) 
WHERE
	(
	0 <> COALESCE (( `OSVersion_osversion_id_Typology`.`finalclass` = 'OSVersion' ), 1 ))
```

