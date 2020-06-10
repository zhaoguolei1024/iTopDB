| 列           | 类型                   | 注释 |
| :----------- | ---------------------- | ---- |
| id           | int [**0**]            |      |
| name         | varchar(255) *NULL* [] |      |
| friendlyname | varchar(255) *NULL*    |      |

```
SELECT DISTINCT
	`FAQCategory`.`id` AS `id`,
	`FAQCategory`.`nam` AS `name`,
	cast( concat( COALESCE ( `FAQCategory`.`nam`, '' )) AS CHAR charset utf8mb4 ) AS `friendlyname` 
FROM
	`faqcategory` `FAQCategory` 
WHERE
	(
	0 <> 1)
```

