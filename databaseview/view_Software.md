| 列           | 类型                                                         | 注释 |
| :----------- | ------------------------------------------------------------ | ---- |
| id           | int [**0**]                                                  |      |
| name         | varchar(255) *NULL* []                                       |      |
| vendor       | varchar(255) *NULL* []                                       |      |
| version      | varchar(255) *NULL* []                                       |      |
| type         | enum('DBServer','Middleware','OtherSoftware','PCSoftware','WebServer') *NULL* |      |
| friendlyname | varchar(511) *NULL*                                          |      |

```
SELECT DISTINCT
	`Software`.`id` AS `id`,
	`Software`.`name` AS `name`,
	`Software`.`vendor` AS `vendor`,
	`Software`.`version` AS `version`,
	`Software`.`type` AS `type`,
	cast(
		concat(
			COALESCE ( `Software`.`name`, '' ),
			COALESCE ( ' ', '' ),
		COALESCE ( `Software`.`version`, '' )) AS CHAR charset utf8mb4 
	) AS `friendlyname` 
FROM
	`software` `Software` 
WHERE
	(
	0 <> 1)
```

