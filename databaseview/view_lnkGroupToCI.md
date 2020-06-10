| 列                         | 类型                                   | 注释 |
| :------------------------- | -------------------------------------- | ---- |
| id                         | int [**0**]                            |      |
| group_id                   | int *NULL* [**0**]                     |      |
| group_name                 | varchar(255) *NULL* []                 |      |
| ci_id                      | int *NULL* [**0**]                     |      |
| ci_name                    | varchar(255) *NULL* []                 |      |
| reason                     | varchar(255) *NULL* []                 |      |
| friendlyname               | varchar(11) []                         |      |
| group_id_friendlyname      | varchar(255) []                        |      |
| group_id_obsolescence_flag | int [**0**]                            |      |
| ci_id_friendlyname         | varchar(511) []                        |      |
| ci_id_finalclass_recall    | varchar(255) *NULL* [**FunctionalCI**] |      |
| ci_id_obsolescence_flag    | int [**0**]                            |      |

```
SELECT DISTINCT
	`lnkGroupToCI`.`id` AS `id`,
	`lnkGroupToCI`.`group_id` AS `group_id`,
	`Group_group_id`.`name` AS `group_name`,
	`lnkGroupToCI`.`ci_id` AS `ci_id`,
	`FunctionalCI_ci_id`.`name` AS `ci_name`,
	`lnkGroupToCI`.`reason` AS `reason`,
	cast( concat( COALESCE ( `lnkGroupToCI`.`group_id`, '' )) AS CHAR charset utf8mb4 ) AS `friendlyname`,
	cast( concat( COALESCE ( `Group_group_id`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `group_id_friendlyname`,
	COALESCE (( `Group_group_id`.`status` = 'obsolete' ), 0 ) AS `group_id_obsolescence_flag`,
IF
	((
			`FunctionalCI_ci_id`.`finalclass` IN ( 'Middleware', 'DBServer', 'WebServer', 'PCSoftware', 'OtherSoftware' )),
		cast(
			concat(
				COALESCE ( `FunctionalCI_ci_id`.`name`, '' ),
				COALESCE ( ' ', '' ),
			COALESCE ( `FunctionalCI_system_id`.`name`, '' )) AS CHAR charset utf8mb4 
		),
	cast( concat( COALESCE ( `FunctionalCI_ci_id`.`name`, '' )) AS CHAR charset utf8mb4 )) AS `ci_id_friendlyname`,
	`FunctionalCI_ci_id`.`finalclass` AS `ci_id_finalclass_recall`,
IF
	((
			`FunctionalCI_ci_id`.`finalclass` = 'FunctionalCI' 
			),
		COALESCE ( 0, 0 ),
	IF
		((
				`FunctionalCI_ci_id`.`finalclass` IN ( 'Hypervisor', 'Farm', 'VirtualMachine' )),
			COALESCE (( `FunctionalCI_ci_id_poly_VirtualDevice`.`status` = 'obsolete' ), 0 ),
		IF
			((
					`FunctionalCI_ci_id`.`finalclass` = 'WebApplication' 
					),
				COALESCE ( COALESCE (( `WebServer_webserver_id_SoftwareInstance`.`status` = 'inactive' ), 0 ), 0 ),
			IF
				((
						`FunctionalCI_ci_id`.`finalclass` = 'DatabaseSchema' 
						),
					COALESCE ( COALESCE (( `DBServer_dbserver_id_SoftwareInstance`.`status` = 'inactive' ), 0 ), 0 ),
				IF
					((
							`FunctionalCI_ci_id`.`finalclass` = 'MiddlewareInstance' 
							),
						COALESCE ( COALESCE (( `Middleware_middleware_id_SoftwareInstance`.`status` = 'inactive' ), 0 ), 0 ),
					IF
						((
								`FunctionalCI_ci_id`.`finalclass` IN ( 'Middleware', 'DBServer', 'WebServer', 'PCSoftware', 'OtherSoftware' )),
							COALESCE (( `FunctionalCI_ci_id_poly_SoftwareInstance`.`status` = 'inactive' ), 0 ),
						IF
							((
									`FunctionalCI_ci_id`.`finalclass` = 'BusinessProcess' 
									),
								COALESCE (( `FunctionalCI_ci_id_poly_BusinessProcess`.`status` = 'inactive' ), 0 ),
							IF
								((
										`FunctionalCI_ci_id`.`finalclass` = 'ApplicationSolution' 
										),
									COALESCE (( `FunctionalCI_ci_id_poly_ApplicationSolution`.`status` = 'inactive' ), 0 ),
								COALESCE (( `FunctionalCI_ci_id_poly_PhysicalDevice`.`status` = 'obsolete' ), 0 ))))))))) AS `ci_id_obsolescence_flag` 
FROM
	((
			`lnkgrouptoci` `lnkGroupToCI`
			JOIN `group` `Group_group_id` ON ((
					`lnkGroupToCI`.`group_id` = `Group_group_id`.`id` 
				)))
		JOIN ((((((((
										`functionalci` `FunctionalCI_ci_id`
										LEFT JOIN (
											`softwareinstance` `FunctionalCI_ci_id_poly_SoftwareInstance`
											JOIN `functionalci` `FunctionalCI_system_id` ON ((
													`FunctionalCI_ci_id_poly_SoftwareInstance`.`functionalci_id` = `FunctionalCI_system_id`.`id` 
													))) ON ((
												`FunctionalCI_ci_id`.`id` = `FunctionalCI_ci_id_poly_SoftwareInstance`.`id` 
											)))
									LEFT JOIN `virtualdevice` `FunctionalCI_ci_id_poly_VirtualDevice` ON ((
											`FunctionalCI_ci_id`.`id` = `FunctionalCI_ci_id_poly_VirtualDevice`.`id` 
										)))
								LEFT JOIN (
									`webapplication` `FunctionalCI_ci_id_poly_WebApplication`
									JOIN `softwareinstance` `WebServer_webserver_id_SoftwareInstance` ON ((
											`FunctionalCI_ci_id_poly_WebApplication`.`webserver_id` = `WebServer_webserver_id_SoftwareInstance`.`id` 
											))) ON ((
										`FunctionalCI_ci_id`.`id` = `FunctionalCI_ci_id_poly_WebApplication`.`id` 
									)))
							LEFT JOIN (
								`databaseschema` `FunctionalCI_ci_id_poly_DatabaseSchema`
								JOIN `softwareinstance` `DBServer_dbserver_id_SoftwareInstance` ON ((
										`FunctionalCI_ci_id_poly_DatabaseSchema`.`dbserver_id` = `DBServer_dbserver_id_SoftwareInstance`.`id` 
										))) ON ((
									`FunctionalCI_ci_id`.`id` = `FunctionalCI_ci_id_poly_DatabaseSchema`.`id` 
								)))
						LEFT JOIN (
							`middlewareinstance` `FunctionalCI_ci_id_poly_MiddlewareInstance`
							JOIN `softwareinstance` `Middleware_middleware_id_SoftwareInstance` ON ((
									`FunctionalCI_ci_id_poly_MiddlewareInstance`.`middleware_id` = `Middleware_middleware_id_SoftwareInstance`.`id` 
									))) ON ((
								`FunctionalCI_ci_id`.`id` = `FunctionalCI_ci_id_poly_MiddlewareInstance`.`id` 
							)))
					LEFT JOIN `businessprocess` `FunctionalCI_ci_id_poly_BusinessProcess` ON ((
							`FunctionalCI_ci_id`.`id` = `FunctionalCI_ci_id_poly_BusinessProcess`.`id` 
						)))
				LEFT JOIN `applicationsolution` `FunctionalCI_ci_id_poly_ApplicationSolution` ON ((
						`FunctionalCI_ci_id`.`id` = `FunctionalCI_ci_id_poly_ApplicationSolution`.`id` 
					)))
			LEFT JOIN `physicaldevice` `FunctionalCI_ci_id_poly_PhysicalDevice` ON ((
					`FunctionalCI_ci_id`.`id` = `FunctionalCI_ci_id_poly_PhysicalDevice`.`id` 
					))) ON ((
				`lnkGroupToCI`.`ci_id` = `FunctionalCI_ci_id`.`id` 
			))) 
WHERE
	((
			0 <> COALESCE (( `WebServer_webserver_id_SoftwareInstance`.`finalclass` = 'WebServer' ), 1 )) 
		AND (
		0 <> COALESCE (( `DBServer_dbserver_id_SoftwareInstance`.`finalclass` = 'DBServer' ), 1 )) 
	AND (
	0 <> COALESCE (( `Middleware_middleware_id_SoftwareInstance`.`finalclass` = 'Middleware' ), 1 )))
```

