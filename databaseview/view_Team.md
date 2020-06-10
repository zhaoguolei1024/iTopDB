| 列                       | 类型                                          | 注释 |
| :----------------------- | --------------------------------------------- | ---- |
| id                       | int [**0**]                                   |      |
| name                     | varchar(255) *NULL* []                        |      |
| status                   | enum('active','inactive') *NULL* [**active**] |      |
| org_id                   | int *NULL* [**0**]                            |      |
| org_name                 | varchar(255) *NULL* []                        |      |
| email                    | varchar(255) *NULL* []                        |      |
| phone                    | varchar(255) *NULL* []                        |      |
| notify                   | enum('no','yes') *NULL* [**yes**]             |      |
| function                 | varchar(255) *NULL* []                        |      |
| finalclass               | varchar(255) *NULL* [**Contact**]             |      |
| friendlyname             | varchar(255) *NULL*                           |      |
| obsolescence_flag        | int [**0**]                                   |      |
| obsolescence_date        | date *NULL*                                   |      |
| org_id_friendlyname      | varchar(255) *NULL*                           |      |
| org_id_obsolescence_flag | int [**0**]                                   |      |

```
SELECT DISTINCT
	`Team_Contact`.`id` AS `id`,
	`Team_Contact`.`name` AS `name`,
	`Team_Contact`.`status` AS `status`,
	`Team_Contact`.`org_id` AS `org_id`,
	`Organization_org_id`.`name` AS `org_name`,
	`Team_Contact`.`email` AS `email`,
	`Team_Contact`.`phone` AS `phone`,
	`Team_Contact`.`notify` AS `notify`,
	`Team_Contact`.`function` AS `function`,
	`Team_Contact`.`finalclass` AS `finalclass`,
	cast( concat( COALESCE ( `Team_Contact`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `friendlyname`,
	COALESCE (( `Team_Contact`.`status` = 'inactive' ), 0 ) AS `obsolescence_flag`,
	`Team_Contact`.`obsolescence_date` AS `obsolescence_date`,
	cast( concat( COALESCE ( `Organization_org_id`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `org_id_friendlyname`,
	COALESCE (( `Organization_org_id`.`status` = 'inactive' ), 0 ) AS `org_id_obsolescence_flag` 
FROM
	(
		`contact` `Team_Contact`
		JOIN `organization` `Organization_org_id` ON ((
				`Team_Contact`.`org_id` = `Organization_org_id`.`id` 
			))) 
WHERE
	(
	0 <> COALESCE (( `Team_Contact`.`finalclass` = 'Team' ), 1 ))
```

