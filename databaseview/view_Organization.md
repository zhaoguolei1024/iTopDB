| 列                            | 类型                                          | 注释 |
| :---------------------------- | --------------------------------------------- | ---- |
| id                            | int [**0**]                                   |      |
| name                          | varchar(255) *NULL* []                        |      |
| code                          | varchar(255) *NULL* []                        |      |
| status                        | enum('active','inactive') *NULL* [**active**] |      |
| parent_id                     | int *NULL* [**0**]                            |      |
| parent_name                   | varchar(255) *NULL* []                        |      |
| deliverymodel_id              | int *NULL* [**0**]                            |      |
| deliverymodel_name            | varchar(255) *NULL* []                        |      |
| friendlyname                  | varchar(255) *NULL*                           |      |
| obsolescence_flag             | int [**0**]                                   |      |
| obsolescence_date             | date *NULL*                                   |      |
| parent_id_friendlyname        | varchar(255) *NULL*                           |      |
| parent_id_obsolescence_flag   | int [**0**]                                   |      |
| deliverymodel_id_friendlyname | varchar(255) *NULL*                           |      |

```
SELECT DISTINCT
	`Organization`.`id` AS `id`,
	`Organization`.`name` AS `name`,
	`Organization`.`code` AS `code`,
	`Organization`.`status` AS `status`,
	`Organization`.`parent_id` AS `parent_id`,
	`Organization_parent_id`.`name` AS `parent_name`,
	`Organization`.`deliverymodel_id` AS `deliverymodel_id`,
	`DeliveryModel_deliverymodel_id`.`name` AS `deliverymodel_name`,
	cast( concat( COALESCE ( `Organization`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `friendlyname`,
	COALESCE (( `Organization`.`status` = 'inactive' ), 0 ) AS `obsolescence_flag`,
	`Organization`.`obsolescence_date` AS `obsolescence_date`,
	cast( concat( COALESCE ( `Organization_parent_id`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `parent_id_friendlyname`,
	COALESCE (( `Organization_parent_id`.`status` = 'inactive' ), 0 ) AS `parent_id_obsolescence_flag`,
	cast( concat( COALESCE ( `DeliveryModel_deliverymodel_id`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `deliverymodel_id_friendlyname` 
FROM
	((
			`organization` `Organization`
			LEFT JOIN `organization` `Organization_parent_id` ON ((
					`Organization`.`parent_id` = `Organization_parent_id`.`id` 
				)))
		LEFT JOIN `deliverymodel` `DeliveryModel_deliverymodel_id` ON ((
				`Organization`.`deliverymodel_id` = `DeliveryModel_deliverymodel_id`.`id` 
			))) 
WHERE
	(
	0 <> 1)
```

