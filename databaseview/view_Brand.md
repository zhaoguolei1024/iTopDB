|              |                                    |      |
| :----------- | ---------------------------------- | ---- |
| 列           | 类型                               | 注释 |
| id           | int [**0**]                        |      |
| name         | varchar(255) *NULL* []             |      |
| finalclass   | varchar(255) *NULL* [**Typology**] |      |
| friendlyname | varchar(255) *NULL*                |      |

```
SELECT DISTINCT
	`Brand_Typology`.`id` AS `id`,
	`Brand_Typology`.`name` AS `name`,
	`Brand_Typology`.`finalclass` AS `finalclass`,
	cast( concat( COALESCE ( `Brand_Typology`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `friendlyname` 
FROM
	`typology` `Brand_Typology` 
WHERE
	(
	0 <> COALESCE (( `Brand_Typology`.`finalclass` = 'Brand' ), 1 ))
```

