| 列                              | 类型                                         | 注释 |
| :------------------------------ | -------------------------------------------- | ---- |
| id                              | int [**0**]                                  |      |
| name                            | varchar(255) *NULL* []                       |      |
| description                     | text *NULL*                                  |      |
| org_id                          | int *NULL* [**0**]                           |      |
| organization_name               | varchar(255) *NULL* []                       |      |
| business_criticity              | enum('high','low','medium') *NULL* [**low**] |      |
| move2production                 | date *NULL*                                  |      |
| middleware_id                   | int *NULL* [**0**]                           |      |
| middleware_name                 | varchar(255) *NULL* []                       |      |
| finalclass                      | varchar(255) *NULL* [**FunctionalCI**]       |      |
| friendlyname                    | varchar(255) *NULL*                          |      |
| obsolescence_flag               | int [**0**]                                  |      |
| obsolescence_date               | date *NULL*                                  |      |
| org_id_friendlyname             | varchar(255) *NULL*                          |      |
| org_id_obsolescence_flag        | int [**0**]                                  |      |
| middleware_id_friendlyname      | varchar(511) *NULL*                          |      |
| middleware_id_obsolescence_flag | int [**0**]                                  |      |

```
SELECT DISTINCT
	`MiddlewareInstance`.`id` AS `id`,
	`MiddlewareInstance_FunctionalCI`.`name` AS `name`,
	`MiddlewareInstance_FunctionalCI`.`description` AS `description`,
	`MiddlewareInstance_FunctionalCI`.`org_id` AS `org_id`,
	`Organization_org_id`.`name` AS `organization_name`,
	`MiddlewareInstance_FunctionalCI`.`business_criticity` AS `business_criticity`,
	`MiddlewareInstance_FunctionalCI`.`move2production` AS `move2production`,
	`MiddlewareInstance`.`middleware_id` AS `middleware_id`,
	`Middleware_middleware_id_FunctionalCI`.`name` AS `middleware_name`,
	`MiddlewareInstance_FunctionalCI`.`finalclass` AS `finalclass`,
	cast( concat( COALESCE ( `MiddlewareInstance_FunctionalCI`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `friendlyname`,
	COALESCE ( COALESCE (( `Middleware_middleware_id_SoftwareInstance`.`status` = 'inactive' ), 0 ), 0 ) AS `obsolescence_flag`,
	`MiddlewareInstance_FunctionalCI`.`obsolescence_date` AS `obsolescence_date`,
	cast( concat( COALESCE ( `Organization_org_id`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `org_id_friendlyname`,
	COALESCE (( `Organization_org_id`.`status` = 'inactive' ), 0 ) AS `org_id_obsolescence_flag`,
	cast(
		concat(
			COALESCE ( `Middleware_middleware_id_FunctionalCI`.`name`, '' ),
			COALESCE ( ' ', '' ),
		COALESCE ( `FunctionalCI_system_id`.`name`, '' )) AS CHAR charset utf8mb4 
	) AS `middleware_id_friendlyname`,
	COALESCE (( `Middleware_middleware_id_SoftwareInstance`.`status` = 'inactive' ), 0 ) AS `middleware_id_obsolescence_flag` 
FROM
	((
			`middlewareinstance` `MiddlewareInstance`
			JOIN ((
					`softwareinstance` `Middleware_middleware_id_SoftwareInstance`
					JOIN `functionalci` `FunctionalCI_system_id` ON ((
							`Middleware_middleware_id_SoftwareInstance`.`functionalci_id` = `FunctionalCI_system_id`.`id` 
						)))
				JOIN `functionalci` `Middleware_middleware_id_FunctionalCI` ON ((
						`Middleware_middleware_id_SoftwareInstance`.`id` = `Middleware_middleware_id_FunctionalCI`.`id` 
						))) ON ((
					`MiddlewareInstance`.`middleware_id` = `Middleware_middleware_id_SoftwareInstance`.`id` 
				)))
		JOIN (
			`functionalci` `MiddlewareInstance_FunctionalCI`
			JOIN `organization` `Organization_org_id` ON ((
					`MiddlewareInstance_FunctionalCI`.`org_id` = `Organization_org_id`.`id` 
					))) ON ((
				`MiddlewareInstance`.`id` = `MiddlewareInstance_FunctionalCI`.`id` 
			))) 
WHERE
	(
	0 <> COALESCE (( `Middleware_middleware_id_SoftwareInstance`.`finalclass` = 'Middleware' ), 1 ))
```

