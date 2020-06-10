| 列           | 类型                            | 注释 |
| :----------- | ------------------------------- | ---- |
| id           | int [**0**]                     |      |
| name         | varchar(255) *NULL* []          |      |
| description  | text *NULL*                     |      |
| finalclass   | varchar(255) *NULL* [**Patch**] |      |
| friendlyname | varchar(255) *NULL*             |      |

```
SELECT DISTINCT
	`Patch`.`id` AS `id`,
	`Patch`.`name` AS `name`,
	`Patch`.`description` AS `description`,
	`Patch`.`finalclass` AS `finalclass`,
	cast( concat( COALESCE ( `Patch`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `friendlyname` 
FROM
	`patch` `Patch` 
WHERE
	(
	0 <> 1)
```

