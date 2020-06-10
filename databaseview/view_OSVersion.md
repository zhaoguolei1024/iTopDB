| 列                       | 类型                               | 注释 |
| :----------------------- | ---------------------------------- | ---- |
| id                       | int [**0**]                        |      |
| name                     | varchar(255) *NULL* []             |      |
| osfamily_id              | int *NULL* [**0**]                 |      |
| osfamily_name            | varchar(255) *NULL* []             |      |
| finalclass               | varchar(255) *NULL* [**Typology**] |      |
| friendlyname             | varchar(255) *NULL*                |      |
| osfamily_id_friendlyname | varchar(255) *NULL*                |      |

```
SELECT DISTINCT
	`OSVersion`.`id` AS `id`,
	`OSVersion_Typology`.`name` AS `name`,
	`OSVersion`.`osfamily_id` AS `osfamily_id`,
	`OSFamily_osfamily_id_Typology`.`name` AS `osfamily_name`,
	`OSVersion_Typology`.`finalclass` AS `finalclass`,
	cast( concat( COALESCE ( `OSVersion_Typology`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `friendlyname`,
	cast( concat( COALESCE ( `OSFamily_osfamily_id_Typology`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `osfamily_id_friendlyname` 
FROM
	((
			`osversion` `OSVersion`
			JOIN `typology` `OSFamily_osfamily_id_Typology` ON ((
					`OSVersion`.`osfamily_id` = `OSFamily_osfamily_id_Typology`.`id` 
				)))
		JOIN `typology` `OSVersion_Typology` ON ((
				`OSVersion`.`id` = `OSVersion_Typology`.`id` 
			))) 
WHERE
	(
	0 <> COALESCE (( `OSFamily_osfamily_id_Typology`.`finalclass` = 'OSFamily' ), 1 ))
```

