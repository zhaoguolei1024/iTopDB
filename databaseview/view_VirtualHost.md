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
	`VirtualHost_VirtualDevice`.`id` AS `id`,
	`VirtualHost_FunctionalCI`.`name` AS `name`,
	`VirtualHost_FunctionalCI`.`description` AS `description`,
	`VirtualHost_FunctionalCI`.`org_id` AS `org_id`,
	`Organization_org_id`.`name` AS `organization_name`,
	`VirtualHost_FunctionalCI`.`business_criticity` AS `business_criticity`,
	`VirtualHost_FunctionalCI`.`move2production` AS `move2production`,
	`VirtualHost_VirtualDevice`.`status` AS `status`,
	`VirtualHost_FunctionalCI`.`finalclass` AS `finalclass`,
	cast( concat( COALESCE ( `VirtualHost_FunctionalCI`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `friendlyname`,
	COALESCE (( `VirtualHost_VirtualDevice`.`status` = 'obsolete' ), 0 ) AS `obsolescence_flag`,
	`VirtualHost_FunctionalCI`.`obsolescence_date` AS `obsolescence_date`,
	cast( concat( COALESCE ( `Organization_org_id`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `org_id_friendlyname`,
	COALESCE (( `Organization_org_id`.`status` = 'inactive' ), 0 ) AS `org_id_obsolescence_flag` 
FROM
	(
		`virtualdevice` `VirtualHost_VirtualDevice`
		JOIN (
			`functionalci` `VirtualHost_FunctionalCI`
			JOIN `organization` `Organization_org_id` ON ((
					`VirtualHost_FunctionalCI`.`org_id` = `Organization_org_id`.`id` 
					))) ON ((
				`VirtualHost_VirtualDevice`.`id` = `VirtualHost_FunctionalCI`.`id` 
			))) 
WHERE
	(
	0 <> COALESCE (( `VirtualHost_VirtualDevice`.`finalclass` IN ( 'Hypervisor', 'Farm', 'VirtualHost' )), 1 ))
```

