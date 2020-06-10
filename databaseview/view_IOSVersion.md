| 列                    | 类型                               | 注释 |
| :-------------------- | ---------------------------------- | ---- |
| id                    | int [**0**]                        |      |
| name                  | varchar(255) *NULL* []             |      |
| brand_id              | int *NULL* [**0**]                 |      |
| brand_name            | varchar(255) *NULL* []             |      |
| finalclass            | varchar(255) *NULL* [**Typology**] |      |
| friendlyname          | varchar(511) *NULL*                |      |
| brand_id_friendlyname | varchar(255) *NULL*                |      |

```
SELECT DISTINCT
	`IOSVersion`.`id` AS `id`,
	`IOSVersion_Typology`.`name` AS `name`,
	`IOSVersion`.`brand_id` AS `brand_id`,
	`Brand_brand_id_Typology`.`name` AS `brand_name`,
	`IOSVersion_Typology`.`finalclass` AS `finalclass`,
	cast(
		concat(
			COALESCE ( `Brand_brand_id_Typology`.`name`, '' ),
			COALESCE ( ' ', '' ),
		COALESCE ( `IOSVersion_Typology`.`name`, '' )) AS CHAR charset utf8mb4 
	) AS `friendlyname`,
	cast( concat( COALESCE ( `Brand_brand_id_Typology`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `brand_id_friendlyname` 
FROM
	((
			`iosversion` `IOSVersion`
			JOIN `typology` `Brand_brand_id_Typology` ON ((
					`IOSVersion`.`brand_id` = `Brand_brand_id_Typology`.`id` 
				)))
		JOIN `typology` `IOSVersion_Typology` ON ((
				`IOSVersion`.`id` = `IOSVersion_Typology`.`id` 
			))) 
WHERE
	(
	0 <> COALESCE (( `Brand_brand_id_Typology`.`finalclass` = 'Brand' ), 1 ))
```

