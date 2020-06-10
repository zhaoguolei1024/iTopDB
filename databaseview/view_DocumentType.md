| 列           | 类型                               | 注释 |
| :----------- | ---------------------------------- | ---- |
| id           | int [**0**]                        |      |
| name         | varchar(255) *NULL* []             |      |
| finalclass   | varchar(255) *NULL* [**Typology**] |      |
| friendlyname | varchar(255) *NULL*                |      |

```
SELECT DISTINCT
	`DocumentType_Typology`.`id` AS `id`,
	`DocumentType_Typology`.`name` AS `name`,
	`DocumentType_Typology`.`finalclass` AS `finalclass`,
	cast( concat( COALESCE ( `DocumentType_Typology`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `friendlyname` 
FROM
	`typology` `DocumentType_Typology` 
WHERE
	(
	0 <> COALESCE (( `DocumentType_Typology`.`finalclass` = 'DocumentType' ), 1 ))
```

