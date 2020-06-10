| 列                       | 类型                                                         | 注释 |
| :----------------------- | ------------------------------------------------------------ | ---- |
| id                       | int [**0**]                                                  |      |
| name                     | varchar(255) *NULL* []                                       |      |
| description              | text *NULL*                                                  |      |
| org_id                   | int *NULL* [**0**]                                           |      |
| organization_name        | varchar(255) *NULL* []                                       |      |
| business_criticity       | enum('high','low','medium') *NULL* [**low**]                 |      |
| move2production          | date *NULL*                                                  |      |
| status                   | enum('implementation','obsolete','production','stock') *NULL* [**production**] |      |
| finalclass               | varchar(255) *NULL* [**FunctionalCI**]                       |      |
| friendlyname             | varchar(255) *NULL*                                          |      |
| obsolescence_flag        | int [**0**]                                                  |      |
| obsolescence_date        | date *NULL*                                                  |      |
| org_id_friendlyname      | varchar(255) *NULL*                                          |      |
| org_id_obsolescence_flag | int [**0**]                                                  |      |

```
SELECT DISTINCT
	`VirtualDevice`.`id` AS `id`,
	`VirtualDevice_FunctionalCI`.`name` AS `name`,
	`VirtualDevice_FunctionalCI`.`description` AS `description`,
	`VirtualDevice_FunctionalCI`.`org_id` AS `org_id`,
	`Organization_org_id`.`name` AS `organization_name`,
	`VirtualDevice_FunctionalCI`.`business_criticity` AS `business_criticity`,
	`VirtualDevice_FunctionalCI`.`move2production` AS `move2production`,
	`VirtualDevice`.`status` AS `status`,
	`VirtualDevice_FunctionalCI`.`finalclass` AS `finalclass`,
	cast( concat( COALESCE ( `VirtualDevice_FunctionalCI`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `friendlyname`,
	COALESCE (( `VirtualDevice`.`status` = 'obsolete' ), 0 ) AS `obsolescence_flag`,
	`VirtualDevice_FunctionalCI`.`obsolescence_date` AS `obsolescence_date`,
	cast( concat( COALESCE ( `Organization_org_id`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `org_id_friendlyname`,
	COALESCE (( `Organization_org_id`.`status` = 'inactive' ), 0 ) AS `org_id_obsolescence_flag` 
FROM
	(
		`virtualdevice` `VirtualDevice`
		JOIN (
			`functionalci` `VirtualDevice_FunctionalCI`
			JOIN `organization` `Organization_org_id` ON ((
					`VirtualDevice_FunctionalCI`.`org_id` = `Organization_org_id`.`id` 
					))) ON ((
				`VirtualDevice`.`id` = `VirtualDevice_FunctionalCI`.`id` 
			))) 
WHERE
	(
	0 <> 1)
```

