| 列           | 类型                               | 注释 |
| :----------- | ---------------------------------- | ---- |
| id           | int [**0**]                        |      |
| name         | varchar(255) *NULL* []             |      |
| finalclass   | varchar(255) *NULL* [**Typology**] |      |
| friendlyname | varchar(511) *NULL*                |      |

```
SELECT DISTINCT
	`Typology`.`id` AS `id`,
	`Typology`.`name` AS `name`,
	`Typology`.`finalclass` AS `finalclass`,
IF
	((
			`Typology`.`finalclass` = 'IOSVersion' 
			),
		cast(
			concat(
				COALESCE ( `Brand_brand_id_Typology`.`name`, '' ),
				COALESCE ( ' ', '' ),
			COALESCE ( `Typology`.`name`, '' )) AS CHAR charset utf8mb4 
		),
	cast( concat( COALESCE ( `Typology`.`name`, '' )) AS CHAR charset utf8mb4 )) AS `friendlyname` 
FROM
	(
		`typology` `Typology`
		LEFT JOIN (
			`iosversion` `Typology_poly_IOSVersion`
			JOIN `typology` `Brand_brand_id_Typology` ON ((
					`Typology_poly_IOSVersion`.`brand_id` = `Brand_brand_id_Typology`.`id` 
					))) ON ((
				`Typology`.`id` = `Typology_poly_IOSVersion`.`id` 
			))) 
WHERE
	(
	0 <> COALESCE (( `Brand_brand_id_Typology`.`finalclass` = 'Brand' ), 1 ))
```

