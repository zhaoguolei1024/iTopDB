| 列                                | 类型                                   | 注释 |
| :-------------------------------- | -------------------------------------- | ---- |
| id                                | int [**0**]                            |      |
| providercontract_id               | int *NULL* [**0**]                     |      |
| providercontract_name             | varchar(255) *NULL* []                 |      |
| functionalci_id                   | int *NULL* [**0**]                     |      |
| functionalci_name                 | varchar(255) *NULL* []                 |      |
| friendlyname                      | varchar(23) []                         |      |
| providercontract_id_friendlyname  | varchar(255) []                        |      |
| functionalci_id_friendlyname      | varchar(511) []                        |      |
| functionalci_id_finalclass_recall | varchar(255) *NULL* [**FunctionalCI**] |      |
| functionalci_id_obsolescence_flag | int [**0**]                            |      |

```
SELECT DISTINCT
	`lnkFunctionalCIToProviderContract`.`id` AS `id`,
	`lnkFunctionalCIToProviderContract`.`providercontract_id` AS `providercontract_id`,
	`ProviderContract_providercontract_id_Contract`.`name` AS `providercontract_name`,
	`lnkFunctionalCIToProviderContract`.`functionalci_id` AS `functionalci_id`,
	`FunctionalCI_functionalci_id`.`name` AS `functionalci_name`,
	cast(
		concat(
			COALESCE ( `lnkFunctionalCIToProviderContract`.`providercontract_id`, '' ),
			COALESCE ( ' ', '' ),
		COALESCE ( `lnkFunctionalCIToProviderContract`.`functionalci_id`, '' )) AS CHAR charset utf8mb4 
	) AS `friendlyname`,
	cast( concat( COALESCE ( `ProviderContract_providercontract_id_Contract`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `providercontract_id_friendlyname`,
IF
	((
			`FunctionalCI_functionalci_id`.`finalclass` IN ( 'Middleware', 'DBServer', 'WebServer', 'PCSoftware', 'OtherSoftware' )),
		cast(
			concat(
				COALESCE ( `FunctionalCI_functionalci_id`.`name`, '' ),
				COALESCE ( ' ', '' ),
			COALESCE ( `FunctionalCI_system_id`.`name`, '' )) AS CHAR charset utf8mb4 
		),
	cast( concat( COALESCE ( `FunctionalCI_functionalci_id`.`name`, '' )) AS CHAR charset utf8mb4 )) AS `functionalci_id_friendlyname`,
	`FunctionalCI_functionalci_id`.`finalclass` AS `functionalci_id_finalclass_recall`,
IF
	((
			`FunctionalCI_functionalci_id`.`finalclass` = 'FunctionalCI' 
			),
		COALESCE ( 0, 0 ),
	IF
		((
				`FunctionalCI_functionalci_id`.`finalclass` IN ( 'Hypervisor', 'Farm', 'VirtualMachine' )),
			COALESCE (( `FunctionalCI_functionalci_id_poly_VirtualDevice`.`status` = 'obsolete' ), 0 ),
		IF
			((
					`FunctionalCI_functionalci_id`.`finalclass` = 'WebApplication' 
					),
				COALESCE ( COALESCE (( `WebServer_webserver_id_SoftwareInstance`.`status` = 'inactive' ), 0 ), 0 ),
			IF
				((
						`FunctionalCI_functionalci_id`.`finalclass` = 'DatabaseSchema' 
						),
					COALESCE ( COALESCE (( `DBServer_dbserver_id_SoftwareInstance`.`status` = 'inactive' ), 0 ), 0 ),
				IF
					((
							`FunctionalCI_functionalci_id`.`finalclass` = 'MiddlewareInstance' 
							),
						COALESCE ( COALESCE (( `Middleware_middleware_id_SoftwareInstance`.`status` = 'inactive' ), 0 ), 0 ),
					IF
						((
								`FunctionalCI_functionalci_id`.`finalclass` IN ( 'Middleware', 'DBServer', 'WebServer', 'PCSoftware', 'OtherSoftware' )),
							COALESCE (( `FunctionalCI_functionalci_id_poly_SoftwareInstance`.`status` = 'inactive' ), 0 ),
						IF
							((
									`FunctionalCI_functionalci_id`.`finalclass` = 'BusinessProcess' 
									),
								COALESCE (( `FunctionalCI_functionalci_id_poly_BusinessProcess`.`status` = 'inactive' ), 0 ),
							IF
								((
										`FunctionalCI_functionalci_id`.`finalclass` = 'ApplicationSolution' 
										),
									COALESCE (( `FunctionalCI_functionalci_id_poly_ApplicationSolution`.`status` = 'inactive' ), 0 ),
								COALESCE (( `FunctionalCI_functionalci_id_poly_PhysicalDevice`.`status` = 'obsolete' ), 0 ))))))))) AS `functionalci_id_obsolescence_flag` 
FROM
	((
			`lnkfunctionalcitoprovidercontract` `lnkFunctionalCIToProviderContract`
			JOIN `contract` `ProviderContract_providercontract_id_Contract` ON ((
					`lnkFunctionalCIToProviderContract`.`providercontract_id` = `ProviderContract_providercontract_id_Contract`.`id` 
				)))
		JOIN ((((((((
										`functionalci` `FunctionalCI_functionalci_id`
										LEFT JOIN (
											`softwareinstance` `FunctionalCI_functionalci_id_poly_SoftwareInstance`
											JOIN `functionalci` `FunctionalCI_system_id` ON ((
													`FunctionalCI_functionalci_id_poly_SoftwareInstance`.`functionalci_id` = `FunctionalCI_system_id`.`id` 
													))) ON ((
												`FunctionalCI_functionalci_id`.`id` = `FunctionalCI_functionalci_id_poly_SoftwareInstance`.`id` 
											)))
									LEFT JOIN `virtualdevice` `FunctionalCI_functionalci_id_poly_VirtualDevice` ON ((
											`FunctionalCI_functionalci_id`.`id` = `FunctionalCI_functionalci_id_poly_VirtualDevice`.`id` 
										)))
								LEFT JOIN (
									`webapplication` `FunctionalCI_functionalci_id_poly_WebApplication`
									JOIN `softwareinstance` `WebServer_webserver_id_SoftwareInstance` ON ((
											`FunctionalCI_functionalci_id_poly_WebApplication`.`webserver_id` = `WebServer_webserver_id_SoftwareInstance`.`id` 
											))) ON ((
										`FunctionalCI_functionalci_id`.`id` = `FunctionalCI_functionalci_id_poly_WebApplication`.`id` 
									)))
							LEFT JOIN (
								`databaseschema` `FunctionalCI_functionalci_id_poly_DatabaseSchema`
								JOIN `softwareinstance` `DBServer_dbserver_id_SoftwareInstance` ON ((
										`FunctionalCI_functionalci_id_poly_DatabaseSchema`.`dbserver_id` = `DBServer_dbserver_id_SoftwareInstance`.`id` 
										))) ON ((
									`FunctionalCI_functionalci_id`.`id` = `FunctionalCI_functionalci_id_poly_DatabaseSchema`.`id` 
								)))
						LEFT JOIN (
							`middlewareinstance` `FunctionalCI_functionalci_id_poly_MiddlewareInstance`
							JOIN `softwareinstance` `Middleware_middleware_id_SoftwareInstance` ON ((
									`FunctionalCI_functionalci_id_poly_MiddlewareInstance`.`middleware_id` = `Middleware_middleware_id_SoftwareInstance`.`id` 
									))) ON ((
								`FunctionalCI_functionalci_id`.`id` = `FunctionalCI_functionalci_id_poly_MiddlewareInstance`.`id` 
							)))
					LEFT JOIN `businessprocess` `FunctionalCI_functionalci_id_poly_BusinessProcess` ON ((
							`FunctionalCI_functionalci_id`.`id` = `FunctionalCI_functionalci_id_poly_BusinessProcess`.`id` 
						)))
				LEFT JOIN `applicationsolution` `FunctionalCI_functionalci_id_poly_ApplicationSolution` ON ((
						`FunctionalCI_functionalci_id`.`id` = `FunctionalCI_functionalci_id_poly_ApplicationSolution`.`id` 
					)))
			LEFT JOIN `physicaldevice` `FunctionalCI_functionalci_id_poly_PhysicalDevice` ON ((
					`FunctionalCI_functionalci_id`.`id` = `FunctionalCI_functionalci_id_poly_PhysicalDevice`.`id` 
					))) ON ((
				`lnkFunctionalCIToProviderContract`.`functionalci_id` = `FunctionalCI_functionalci_id`.`id` 
			))) 
WHERE
	((
			0 <> COALESCE (( `ProviderContract_providercontract_id_Contract`.`finalclass` = 'ProviderContract' ), 1 )) 
		AND (
		0 <> COALESCE (( `WebServer_webserver_id_SoftwareInstance`.`finalclass` = 'WebServer' ), 1 )) 
		AND (
		0 <> COALESCE (( `DBServer_dbserver_id_SoftwareInstance`.`finalclass` = 'DBServer' ), 1 )) 
	AND (
	0 <> COALESCE (( `Middleware_middleware_id_SoftwareInstance`.`finalclass` = 'Middleware' ), 1 )))
```

