| 列                       | 类型                                         | 注释 |
| :----------------------- | -------------------------------------------- | ---- |
| id                       | int [**0**]                                  |      |
| name                     | varchar(255) *NULL* []                       |      |
| description              | text *NULL*                                  |      |
| org_id                   | int *NULL* [**0**]                           |      |
| organization_name        | varchar(255) *NULL* []                       |      |
| business_criticity       | enum('high','low','medium') *NULL* [**low**] |      |
| move2production          | date *NULL*                                  |      |
| finalclass               | varchar(255) *NULL* [**FunctionalCI**]       |      |
| friendlyname             | varchar(511) []                              |      |
| obsolescence_flag        | int [**0**]                                  |      |
| obsolescence_date        | date *NULL*                                  |      |
| org_id_friendlyname      | varchar(255) []                              |      |
| org_id_obsolescence_flag | int [**0**]                                  |      |

```
SELECT DISTINCT
	`FunctionalCI`.`id` AS `id`,
	`FunctionalCI`.`name` AS `name`,
	`FunctionalCI`.`description` AS `description`,
	`FunctionalCI`.`org_id` AS `org_id`,
	`Organization_org_id`.`name` AS `organization_name`,
	`FunctionalCI`.`business_criticity` AS `business_criticity`,
	`FunctionalCI`.`move2production` AS `move2production`,
	`FunctionalCI`.`finalclass` AS `finalclass`,
IF
	((
			`FunctionalCI`.`finalclass` IN ( 'Middleware', 'DBServer', 'WebServer', 'PCSoftware', 'OtherSoftware' )),
		cast(
			concat(
				COALESCE ( `FunctionalCI`.`name`, '' ),
				COALESCE ( ' ', '' ),
			COALESCE ( `FunctionalCI_system_id`.`name`, '' )) AS CHAR charset utf8mb4 
		),
	cast( concat( COALESCE ( `FunctionalCI`.`name`, '' )) AS CHAR charset utf8mb4 )) AS `friendlyname`,
IF
	((
			`FunctionalCI`.`finalclass` = 'FunctionalCI' 
			),
		COALESCE ( 0, 0 ),
	IF
		((
				`FunctionalCI`.`finalclass` IN ( 'Hypervisor', 'Farm', 'VirtualMachine' )),
			COALESCE (( `FunctionalCI_poly_VirtualDevice`.`status` = 'obsolete' ), 0 ),
		IF
			((
					`FunctionalCI`.`finalclass` = 'WebApplication' 
					),
				COALESCE ( COALESCE (( `WebServer_webserver_id_SoftwareInstance`.`status` = 'inactive' ), 0 ), 0 ),
			IF
				((
						`FunctionalCI`.`finalclass` = 'DatabaseSchema' 
						),
					COALESCE ( COALESCE (( `DBServer_dbserver_id_SoftwareInstance`.`status` = 'inactive' ), 0 ), 0 ),
				IF
					((
							`FunctionalCI`.`finalclass` = 'MiddlewareInstance' 
							),
						COALESCE ( COALESCE (( `Middleware_middleware_id_SoftwareInstance`.`status` = 'inactive' ), 0 ), 0 ),
					IF
						((
								`FunctionalCI`.`finalclass` IN ( 'Middleware', 'DBServer', 'WebServer', 'PCSoftware', 'OtherSoftware' )),
							COALESCE (( `FunctionalCI_poly_SoftwareInstance`.`status` = 'inactive' ), 0 ),
						IF
							((
									`FunctionalCI`.`finalclass` = 'BusinessProcess' 
									),
								COALESCE (( `FunctionalCI_poly_BusinessProcess`.`status` = 'inactive' ), 0 ),
							IF
								((
										`FunctionalCI`.`finalclass` = 'ApplicationSolution' 
										),
									COALESCE (( `FunctionalCI_poly_ApplicationSolution`.`status` = 'inactive' ), 0 ),
								COALESCE (( `FunctionalCI_poly_PhysicalDevice`.`status` = 'obsolete' ), 0 ))))))))) AS `obsolescence_flag`,
	`FunctionalCI`.`obsolescence_date` AS `obsolescence_date`,
	cast( concat( COALESCE ( `Organization_org_id`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `org_id_friendlyname`,
	COALESCE (( `Organization_org_id`.`status` = 'inactive' ), 0 ) AS `org_id_obsolescence_flag` 
FROM
	(((((((((
										`functionalci` `FunctionalCI`
										JOIN `organization` `Organization_org_id` ON ((
												`FunctionalCI`.`org_id` = `Organization_org_id`.`id` 
											)))
									LEFT JOIN (
										`softwareinstance` `FunctionalCI_poly_SoftwareInstance`
										JOIN `functionalci` `FunctionalCI_system_id` ON ((
												`FunctionalCI_poly_SoftwareInstance`.`functionalci_id` = `FunctionalCI_system_id`.`id` 
												))) ON ((
											`FunctionalCI`.`id` = `FunctionalCI_poly_SoftwareInstance`.`id` 
										)))
								LEFT JOIN `virtualdevice` `FunctionalCI_poly_VirtualDevice` ON ((
										`FunctionalCI`.`id` = `FunctionalCI_poly_VirtualDevice`.`id` 
									)))
							LEFT JOIN (
								`webapplication` `FunctionalCI_poly_WebApplication`
								JOIN `softwareinstance` `WebServer_webserver_id_SoftwareInstance` ON ((
										`FunctionalCI_poly_WebApplication`.`webserver_id` = `WebServer_webserver_id_SoftwareInstance`.`id` 
										))) ON ((
									`FunctionalCI`.`id` = `FunctionalCI_poly_WebApplication`.`id` 
								)))
						LEFT JOIN (
							`databaseschema` `FunctionalCI_poly_DatabaseSchema`
							JOIN `softwareinstance` `DBServer_dbserver_id_SoftwareInstance` ON ((
									`FunctionalCI_poly_DatabaseSchema`.`dbserver_id` = `DBServer_dbserver_id_SoftwareInstance`.`id` 
									))) ON ((
								`FunctionalCI`.`id` = `FunctionalCI_poly_DatabaseSchema`.`id` 
							)))
					LEFT JOIN (
						`middlewareinstance` `FunctionalCI_poly_MiddlewareInstance`
						JOIN `softwareinstance` `Middleware_middleware_id_SoftwareInstance` ON ((
								`FunctionalCI_poly_MiddlewareInstance`.`middleware_id` = `Middleware_middleware_id_SoftwareInstance`.`id` 
								))) ON ((
							`FunctionalCI`.`id` = `FunctionalCI_poly_MiddlewareInstance`.`id` 
						)))
				LEFT JOIN `businessprocess` `FunctionalCI_poly_BusinessProcess` ON ((
						`FunctionalCI`.`id` = `FunctionalCI_poly_BusinessProcess`.`id` 
					)))
			LEFT JOIN `applicationsolution` `FunctionalCI_poly_ApplicationSolution` ON ((
					`FunctionalCI`.`id` = `FunctionalCI_poly_ApplicationSolution`.`id` 
				)))
		LEFT JOIN `physicaldevice` `FunctionalCI_poly_PhysicalDevice` ON ((
				`FunctionalCI`.`id` = `FunctionalCI_poly_PhysicalDevice`.`id` 
			))) 
WHERE
	((
			0 <> COALESCE (( `WebServer_webserver_id_SoftwareInstance`.`finalclass` = 'WebServer' ), 1 )) 
		AND (
		0 <> COALESCE (( `DBServer_dbserver_id_SoftwareInstance`.`finalclass` = 'DBServer' ), 1 )) 
	AND (
	0 <> COALESCE (( `Middleware_middleware_id_SoftwareInstance`.`finalclass` = 'Middleware' ), 1 )))
```

