| 列           | 类型                               | 注释 |
| :----------- | ---------------------------------- | ---- |
| id           | int [**0**]                        |      |
| name         | varchar(255) *NULL* []             |      |
| finalclass   | varchar(255) *NULL* [**Typology**] |      |
| friendlyname | varchar(255) *NULL*                |      |

```
SELECT DISTINCT
	`OSFamily_Typology`.`id` AS `id`,
	`OSFamily_Typology`.`name` AS `name`,
	`OSFamily_Typology`.`finalclass` AS `finalclass`,
	cast( concat( COALESCE ( `OSFamily_Typology`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `friendlyname` 
FROM
	`typology` `OSFamily_Typology` 
WHERE
	(
	0 <> COALESCE (( `OSFamily_Typology`.`finalclass` = 'OSFamily' ), 1 ))
```

