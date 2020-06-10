| 列                                   | 类型                                         | 注释 |
| :----------------------------------- | -------------------------------------------- | ---- |
| id                                   | int [**0**]                                  |      |
| name                                 | varchar(255) *NULL* []                       |      |
| description                          | text *NULL*                                  |      |
| org_id                               | int *NULL* [**0**]                           |      |
| organization_name                    | varchar(255) *NULL* []                       |      |
| business_criticity                   | enum('high','low','medium') *NULL* [**low**] |      |
| move2production                      | date *NULL*                                  |      |
| system_id                            | int *NULL* [**0**]                           |      |
| system_name                          | varchar(255) *NULL* []                       |      |
| software_id                          | int *NULL* [**0**]                           |      |
| software_name                        | varchar(255) *NULL* []                       |      |
| softwarelicence_id                   | int *NULL* [**0**]                           |      |
| softwarelicence_name                 | varchar(255) *NULL* []                       |      |
| path                                 | varchar(255) *NULL* []                       |      |
| status                               | enum('active','inactive') *NULL*             |      |
| finalclass                           | varchar(255) *NULL* [**FunctionalCI**]       |      |
| friendlyname                         | varchar(511) []                              |      |
| obsolescence_flag                    | int [**0**]                                  |      |
| obsolescence_date                    | date *NULL*                                  |      |
| org_id_friendlyname                  | varchar(255) []                              |      |
| org_id_obsolescence_flag             | int [**0**]                                  |      |
| system_id_friendlyname               | varchar(511) []                              |      |
| system_id_finalclass_recall          | varchar(255) *NULL* [**FunctionalCI**]       |      |
| system_id_obsolescence_flag          | int [**0**]                                  |      |
| software_id_friendlyname             | varchar(511) []                              |      |
| softwarelicence_id_friendlyname      | varchar(255) []                              |      |
| softwarelicence_id_obsolescence_flag | int [**0**]                                  |      |

```
SELECT DISTINCT
	`SoftwareInstance`.`id` AS `id`,
	`SoftwareInstance_FunctionalCI`.`name` AS `name`,
	`SoftwareInstance_FunctionalCI`.`description` AS `description`,
	`SoftwareInstance_FunctionalCI`.`org_id` AS `org_id`,
	`Organization_org_id`.`name` AS `organization_name`,
	`SoftwareInstance_FunctionalCI`.`business_criticity` AS `business_criticity`,
	`SoftwareInstance_FunctionalCI`.`move2production` AS `move2production`,
	`SoftwareInstance`.`functionalci_id` AS `system_id`,
	`FunctionalCI_system_id`.`name` AS `system_name`,
	`SoftwareInstance`.`software_id` AS `software_id`,
	`Software_software_id`.`name` AS `software_name`,
	`SoftwareInstance`.`softwarelicence_id` AS `softwarelicence_id`,
	`SoftwareLicence_softwarelicence_id_Licence`.`name` AS `softwarelicence_name`,
	`SoftwareInstance`.`path` AS `path`,
	`SoftwareInstance`.`status` AS `status`,
	`SoftwareInstance_FunctionalCI`.`finalclass` AS `finalclass`,
	cast(
		concat(
			COALESCE ( `SoftwareInstance_FunctionalCI`.`name`, '' ),
			COALESCE ( ' ', '' ),
		COALESCE ( `FunctionalCI_system_id`.`name`, '' )) AS CHAR charset utf8mb4 
	) AS `friendlyname`,
	COALESCE (( `SoftwareInstance`.`status` = 'inactive' ), 0 ) AS `obsolescence_flag`,
	`SoftwareInstance_FunctionalCI`.`obsolescence_date` AS `obsolescence_date`,
	cast( concat( COALESCE ( `Organization_org_id`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `org_id_friendlyname`,
	COALESCE (( `Organization_org_id`.`status` = 'inactive' ), 0 ) AS `org_id_obsolescence_flag`,
IF
	((
			`FunctionalCI_system_id`.`finalclass` IN ( 'Middleware', 'DBServer', 'WebServer', 'PCSoftware', 'OtherSoftware' )),
		cast(
			concat(
				COALESCE ( `FunctionalCI_system_id`.`name`, '' ),
				COALESCE ( ' ', '' ),
			COALESCE ( `FunctionalCI_system_id1`.`name`, '' )) AS CHAR charset utf8mb4 
		),
	cast( concat( COALESCE ( `FunctionalCI_system_id`.`name`, '' )) AS CHAR charset utf8mb4 )) AS `system_id_friendlyname`,
	`FunctionalCI_system_id`.`finalclass` AS `system_id_finalclass_recall`,
IF
	((
			`FunctionalCI_system_id`.`finalclass` = 'FunctionalCI' 
			),
		COALESCE ( 0, 0 ),
	IF
		((
				`FunctionalCI_system_id`.`finalclass` IN ( 'Hypervisor', 'Farm', 'VirtualMachine' )),
			COALESCE (( `FunctionalCI_system_id_poly_VirtualDevice`.`status` = 'obsolete' ), 0 ),
		IF
			((
					`FunctionalCI_system_id`.`finalclass` = 'WebApplication' 
					),
				COALESCE ( COALESCE (( `WebServer_webserver_id_SoftwareInstance`.`status` = 'inactive' ), 0 ), 0 ),
			IF
				((
						`FunctionalCI_system_id`.`finalclass` = 'DatabaseSchema' 
						),
					COALESCE ( COALESCE (( `DBServer_dbserver_id_SoftwareInstance`.`status` = 'inactive' ), 0 ), 0 ),
				IF
					((
							`FunctionalCI_system_id`.`finalclass` = 'MiddlewareInstance' 
							),
						COALESCE ( COALESCE (( `Middleware_middleware_id_SoftwareInstance`.`status` = 'inactive' ), 0 ), 0 ),
					IF
						((
								`FunctionalCI_system_id`.`finalclass` IN ( 'Middleware', 'DBServer', 'WebServer', 'PCSoftware', 'OtherSoftware' )),
							COALESCE (( `FunctionalCI_system_id_poly_SoftwareInstance`.`status` = 'inactive' ), 0 ),
						IF
							((
									`FunctionalCI_system_id`.`finalclass` = 'BusinessProcess' 
									),
								COALESCE (( `FunctionalCI_system_id_poly_BusinessProcess`.`status` = 'inactive' ), 0 ),
							IF
								((
										`FunctionalCI_system_id`.`finalclass` = 'ApplicationSolution' 
										),
									COALESCE (( `FunctionalCI_system_id_poly_ApplicationSolution`.`status` = 'inactive' ), 0 ),
								COALESCE (( `FunctionalCI_system_id_poly_PhysicalDevice`.`status` = 'obsolete' ), 0 ))))))))) AS `system_id_obsolescence_flag`,
	cast(
		concat(
			COALESCE ( `Software_software_id`.`name`, '' ),
			COALESCE ( ' ', '' ),
		COALESCE ( `Software_software_id`.`version`, '' )) AS CHAR charset utf8mb4 
	) AS `software_id_friendlyname`,
	cast( concat( COALESCE ( `SoftwareLicence_softwarelicence_id_Licence`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `softwarelicence_id_friendlyname`,
	COALESCE (((
				`SoftwareLicence_softwarelicence_id_Licence`.`perpetual` = 'no' 
				) 
			AND (( `SoftwareLicence_softwarelicence_id_Licence`.`end_date` IS NULL ) = 0 ) 
			AND (
			`SoftwareLicence_softwarelicence_id_Licence`.`end_date` < date_format(( now() - INTERVAL 15 MONTH ), '%Y-%m-%d 00:00:00' ))),
		0 
	) AS `softwarelicence_id_obsolescence_flag` 
FROM
	((((
					`softwareinstance` `SoftwareInstance`
					JOIN ((((((((
													`functionalci` `FunctionalCI_system_id`
													LEFT JOIN (
														`softwareinstance` `FunctionalCI_system_id_poly_SoftwareInstance`
														JOIN `functionalci` `FunctionalCI_system_id1` ON ((
																`FunctionalCI_system_id_poly_SoftwareInstance`.`functionalci_id` = `FunctionalCI_system_id1`.`id` 
																))) ON ((
															`FunctionalCI_system_id`.`id` = `FunctionalCI_system_id_poly_SoftwareInstance`.`id` 
														)))
												LEFT JOIN `virtualdevice` `FunctionalCI_system_id_poly_VirtualDevice` ON ((
														`FunctionalCI_system_id`.`id` = `FunctionalCI_system_id_poly_VirtualDevice`.`id` 
													)))
											LEFT JOIN (
												`webapplication` `FunctionalCI_system_id_poly_WebApplication`
												JOIN `softwareinstance` `WebServer_webserver_id_SoftwareInstance` ON ((
														`FunctionalCI_system_id_poly_WebApplication`.`webserver_id` = `WebServer_webserver_id_SoftwareInstance`.`id` 
														))) ON ((
													`FunctionalCI_system_id`.`id` = `FunctionalCI_system_id_poly_WebApplication`.`id` 
												)))
										LEFT JOIN (
											`databaseschema` `FunctionalCI_system_id_poly_DatabaseSchema`
											JOIN `softwareinstance` `DBServer_dbserver_id_SoftwareInstance` ON ((
													`FunctionalCI_system_id_poly_DatabaseSchema`.`dbserver_id` = `DBServer_dbserver_id_SoftwareInstance`.`id` 
													))) ON ((
												`FunctionalCI_system_id`.`id` = `FunctionalCI_system_id_poly_DatabaseSchema`.`id` 
											)))
									LEFT JOIN (
										`middlewareinstance` `FunctionalCI_system_id_poly_MiddlewareInstance`
										JOIN `softwareinstance` `Middleware_middleware_id_SoftwareInstance` ON ((
												`FunctionalCI_system_id_poly_MiddlewareInstance`.`middleware_id` = `Middleware_middleware_id_SoftwareInstance`.`id` 
												))) ON ((
											`FunctionalCI_system_id`.`id` = `FunctionalCI_system_id_poly_MiddlewareInstance`.`id` 
										)))
								LEFT JOIN `businessprocess` `FunctionalCI_system_id_poly_BusinessProcess` ON ((
										`FunctionalCI_system_id`.`id` = `FunctionalCI_system_id_poly_BusinessProcess`.`id` 
									)))
							LEFT JOIN `applicationsolution` `FunctionalCI_system_id_poly_ApplicationSolution` ON ((
									`FunctionalCI_system_id`.`id` = `FunctionalCI_system_id_poly_ApplicationSolution`.`id` 
								)))
						LEFT JOIN `physicaldevice` `FunctionalCI_system_id_poly_PhysicalDevice` ON ((
								`FunctionalCI_system_id`.`id` = `FunctionalCI_system_id_poly_PhysicalDevice`.`id` 
								))) ON ((
							`SoftwareInstance`.`functionalci_id` = `FunctionalCI_system_id`.`id` 
						)))
				LEFT JOIN `software` `Software_software_id` ON ((
						`SoftwareInstance`.`software_id` = `Software_software_id`.`id` 
					)))
			LEFT JOIN `licence` `SoftwareLicence_softwarelicence_id_Licence` ON ((
					`SoftwareInstance`.`softwarelicence_id` = `SoftwareLicence_softwarelicence_id_Licence`.`id` 
				)))
		JOIN (
			`functionalci` `SoftwareInstance_FunctionalCI`
			JOIN `organization` `Organization_org_id` ON ((
					`SoftwareInstance_FunctionalCI`.`org_id` = `Organization_org_id`.`id` 
					))) ON ((
				`SoftwareInstance`.`id` = `SoftwareInstance_FunctionalCI`.`id` 
			))) 
WHERE
	((
			0 <> COALESCE (( `WebServer_webserver_id_SoftwareInstance`.`finalclass` = 'WebServer' ), 1 )) 
		AND (
		0 <> COALESCE (( `DBServer_dbserver_id_SoftwareInstance`.`finalclass` = 'DBServer' ), 1 )) 
		AND (
		0 <> COALESCE (( `Middleware_middleware_id_SoftwareInstance`.`finalclass` = 'Middleware' ), 1 )) 
	AND (
	0 <> COALESCE (( `SoftwareLicence_softwarelicence_id_Licence`.`finalclass` = 'SoftwareLicence' ), 1 )))
```

