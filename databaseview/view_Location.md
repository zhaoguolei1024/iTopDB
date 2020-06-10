| 列                       | 类型                                          | 注释 |
| :----------------------- | --------------------------------------------- | ---- |
| id                       | int [**0**]                                   |      |
| name                     | varchar(255) *NULL* []                        |      |
| status                   | enum('active','inactive') *NULL* [**active**] |      |
| org_id                   | int *NULL* [**0**]                            |      |
| org_name                 | varchar(255) *NULL* []                        |      |
| address                  | text *NULL*                                   |      |
| postal_code              | varchar(255) *NULL* []                        |      |
| city                     | varchar(255) *NULL* []                        |      |
| country                  | varchar(255) *NULL* []                        |      |
| friendlyname             | varchar(255) *NULL*                           |      |
| obsolescence_flag        | int [**0**]                                   |      |
| obsolescence_date        | date *NULL*                                   |      |
| org_id_friendlyname      | varchar(255) *NULL*                           |      |
| org_id_obsolescence_flag | int [**0**]                                   |      |

```
SELECT DISTINCT
	`Location`.`id` AS `id`,
	`Location`.`name` AS `name`,
	`Location`.`status` AS `status`,
	`Location`.`org_id` AS `org_id`,
	`Organization_org_id`.`name` AS `org_name`,
	`Location`.`address` AS `address`,
	`Location`.`postal_code` AS `postal_code`,
	`Location`.`city` AS `city`,
	`Location`.`country` AS `country`,
	cast( concat( COALESCE ( `Location`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `friendlyname`,
	COALESCE (( `Location`.`status` = 'inactive' ), 0 ) AS `obsolescence_flag`,
	`Location`.`obsolescence_date` AS `obsolescence_date`,
	cast( concat( COALESCE ( `Organization_org_id`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `org_id_friendlyname`,
	COALESCE (( `Organization_org_id`.`status` = 'inactive' ), 0 ) AS `org_id_obsolescence_flag` 
FROM
	(
		`location` `Location`
		JOIN `organization` `Organization_org_id` ON ((
				`Location`.`org_id` = `Organization_org_id`.`id` 
			))) 
WHERE
	(
	0 <> 1)
```

