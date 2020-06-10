| 列                         | 类型                   | 注释 |
| :------------------------- | ---------------------- | ---- |
| id                         | int [**0**]            |      |
| name                       | varchar(255) *NULL* [] |      |
| icon                       | varchar(255) *NULL*    |      |
| friendlyname               | varchar(255) *NULL*    |      |
| ServiceFamilyicon_data     | longblob *NULL*        |      |
| ServiceFamilyicon_filename | varchar(255) *NULL*    |      |

```
SELECT DISTINCT
	`ServiceFamily`.`id` AS `id`,
	`ServiceFamily`.`name` AS `name`,
	`ServiceFamily`.`icon_mimetype` AS `icon`,
	cast( concat( COALESCE ( `ServiceFamily`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `friendlyname`,
	`ServiceFamily`.`icon_data` AS `ServiceFamilyicon_data`,
	`ServiceFamily`.`icon_filename` AS `ServiceFamilyicon_filename` 
FROM
	`servicefamily` `ServiceFamily` 
WHERE
	(
	0 <> 1)
```

