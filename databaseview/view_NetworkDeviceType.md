| 列           | 类型                               | 注释 |
| :----------- | ---------------------------------- | ---- |
| id           | int [**0**]                        |      |
| name         | varchar(255) *NULL* []             |      |
| finalclass   | varchar(255) *NULL* [**Typology**] |      |
| friendlyname | varchar(255) *NULL*                |      |

```
SELECT DISTINCT
	`NetworkDeviceType_Typology`.`id` AS `id`,
	`NetworkDeviceType_Typology`.`name` AS `name`,
	`NetworkDeviceType_Typology`.`finalclass` AS `finalclass`,
	cast( concat( COALESCE ( `NetworkDeviceType_Typology`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `friendlyname` 
FROM
	`typology` `NetworkDeviceType_Typology` 
WHERE
	(
	0 <> COALESCE (( `NetworkDeviceType_Typology`.`finalclass` = 'NetworkDeviceType' ), 1 ))
```

