| 列                       | 类型                   | 注释 |
| :----------------------- | ---------------------- | ---- |
| id                       | int [**0**]            |      |
| name                     | varchar(255) *NULL* [] |      |
| org_id                   | int *NULL* [**0**]     |      |
| organization_name        | varchar(255) *NULL* [] |      |
| description              | text *NULL*            |      |
| friendlyname             | varchar(255) *NULL*    |      |
| org_id_friendlyname      | varchar(255) *NULL*    |      |
| org_id_obsolescence_flag | int [**0**]            |      |

```
SELECT DISTINCT
	`DeliveryModel`.`id` AS `id`,
	`DeliveryModel`.`name` AS `name`,
	`DeliveryModel`.`org_id` AS `org_id`,
	`Organization_org_id`.`name` AS `organization_name`,
	`DeliveryModel`.`description` AS `description`,
	cast( concat( COALESCE ( `DeliveryModel`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `friendlyname`,
	cast( concat( COALESCE ( `Organization_org_id`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `org_id_friendlyname`,
	COALESCE (( `Organization_org_id`.`status` = 'inactive' ), 0 ) AS `org_id_obsolescence_flag` 
FROM
	(
		`deliverymodel` `DeliveryModel`
		JOIN `organization` `Organization_org_id` ON ((
				`DeliveryModel`.`org_id` = `Organization_org_id`.`id` 
			))) 
WHERE
	(
	0 <> 1)
```

