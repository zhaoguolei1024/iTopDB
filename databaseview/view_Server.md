| 列                             | 类型                                                         | 注释 |
| :----------------------------- | ------------------------------------------------------------ | ---- |
| id                             | int [**0**]                                                  |      |
| name                           | varchar(255) *NULL* []                                       |      |
| description                    | text *NULL*                                                  |      |
| org_id                         | int *NULL* [**0**]                                           |      |
| organization_name              | varchar(255) *NULL* []                                       |      |
| business_criticity             | enum('high','low','medium') *NULL* [**low**]                 |      |
| move2production                | date *NULL*                                                  |      |
| serialnumber                   | varchar(255) *NULL* []                                       |      |
| location_id                    | int *NULL* [**0**]                                           |      |
| location_name                  | varchar(255) *NULL* []                                       |      |
| status                         | enum('implementation','obsolete','production','stock') *NULL* [**production**] |      |
| brand_id                       | int *NULL* [**0**]                                           |      |
| brand_name                     | varchar(255) *NULL* []                                       |      |
| model_id                       | int *NULL* [**0**]                                           |      |
| model_name                     | varchar(255) *NULL* []                                       |      |
| asset_number                   | varchar(255) *NULL* []                                       |      |
| purchase_date                  | date *NULL*                                                  |      |
| end_of_warranty                | date *NULL*                                                  |      |
| rack_id                        | int *NULL* [**0**]                                           |      |
| rack_name                      | varchar(255) *NULL* []                                       |      |
| enclosure_id                   | int *NULL* [**0**]                                           |      |
| enclosure_name                 | varchar(255) *NULL* []                                       |      |
| nb_u                           | int *NULL*                                                   |      |
| managementip                   | varchar(255) *NULL* []                                       |      |
| powerA_id                      | int *NULL* [**0**]                                           |      |
| powerA_name                    | varchar(255) *NULL* []                                       |      |
| powerB_id                      | int *NULL* [**0**]                                           |      |
| powerB_name                    | varchar(255) *NULL* []                                       |      |
| redundancy                     | varchar(20) *NULL* [**1**]                                   |      |
| osfamily_id                    | int *NULL* [**0**]                                           |      |
| osfamily_name                  | varchar(255) *NULL* []                                       |      |
| osversion_id                   | int *NULL* [**0**]                                           |      |
| osversion_name                 | varchar(255) *NULL* []                                       |      |
| oslicence_id                   | int *NULL* [**0**]                                           |      |
| oslicence_name                 | varchar(255) *NULL* []                                       |      |
| cpu                            | varchar(255) *NULL* []                                       |      |
| ram                            | varchar(255) *NULL* []                                       |      |
| finalclass                     | varchar(255) *NULL* [**FunctionalCI**]                       |      |
| friendlyname                   | varchar(255) *NULL*                                          |      |
| obsolescence_flag              | int [**0**]                                                  |      |
| obsolescence_date              | date *NULL*                                                  |      |
| org_id_friendlyname            | varchar(255) *NULL*                                          |      |
| org_id_obsolescence_flag       | int [**0**]                                                  |      |
| location_id_friendlyname       | varchar(255) *NULL*                                          |      |
| location_id_obsolescence_flag  | int [**0**]                                                  |      |
| brand_id_friendlyname          | varchar(255) *NULL*                                          |      |
| model_id_friendlyname          | varchar(255) *NULL*                                          |      |
| rack_id_friendlyname           | varchar(255) *NULL*                                          |      |
| rack_id_obsolescence_flag      | int [**0**]                                                  |      |
| enclosure_id_friendlyname      | varchar(255) *NULL*                                          |      |
| enclosure_id_obsolescence_flag | int [**0**]                                                  |      |
| powerA_id_friendlyname         | varchar(255) *NULL*                                          |      |
| powerA_id_finalclass_recall    | varchar(255) *NULL* [**FunctionalCI**]                       |      |
| powerA_id_obsolescence_flag    | int [**0**]                                                  |      |
| powerB_id_friendlyname         | varchar(255) *NULL*                                          |      |
| powerB_id_finalclass_recall    | varchar(255) *NULL* [**FunctionalCI**]                       |      |
| powerB_id_obsolescence_flag    | int [**0**]                                                  |      |
| osfamily_id_friendlyname       | varchar(255) *NULL*                                          |      |
| osversion_id_friendlyname      | varchar(255) *NULL*                                          |      |
| oslicence_id_friendlyname      | varchar(255) *NULL*                                          |      |
| oslicence_id_obsolescence_flag | int [**0**]                                                  |      |

```
SELECT DISTINCT
	`Server`.`id` AS `id`,
	`Server_FunctionalCI`.`name` AS `name`,
	`Server_FunctionalCI`.`description` AS `description`,
	`Server_FunctionalCI`.`org_id` AS `org_id`,
	`Organization_org_id`.`name` AS `organization_name`,
	`Server_FunctionalCI`.`business_criticity` AS `business_criticity`,
	`Server_FunctionalCI`.`move2production` AS `move2production`,
	`Server_PhysicalDevice`.`serialnumber` AS `serialnumber`,
	`Server_PhysicalDevice`.`location_id` AS `location_id`,
	`Location_location_id`.`name` AS `location_name`,
	`Server_PhysicalDevice`.`status` AS `status`,
	`Server_PhysicalDevice`.`brand_id` AS `brand_id`,
	`Brand_brand_id_Typology`.`name` AS `brand_name`,
	`Server_PhysicalDevice`.`model_id` AS `model_id`,
	`Model_model_id_Typology`.`name` AS `model_name`,
	`Server_PhysicalDevice`.`asset_number` AS `asset_number`,
	`Server_PhysicalDevice`.`purchase_date` AS `purchase_date`,
	`Server_PhysicalDevice`.`end_of_warranty` AS `end_of_warranty`,
	`Server_DatacenterDevice`.`rack_id` AS `rack_id`,
	`Rack_rack_id_FunctionalCI`.`name` AS `rack_name`,
	`Server_DatacenterDevice`.`enclosure_id` AS `enclosure_id`,
	`Enclosure_enclosure_id_FunctionalCI`.`name` AS `enclosure_name`,
	`Server_DatacenterDevice`.`nb_u` AS `nb_u`,
	`Server_DatacenterDevice`.`managementip` AS `managementip`,
	`Server_DatacenterDevice`.`powera_id` AS `powerA_id`,
	`PowerConnection_powerA_id_FunctionalCI`.`name` AS `powerA_name`,
	`Server_DatacenterDevice`.`powerB_id` AS `powerB_id`,
	`PowerConnection_powerB_id_FunctionalCI`.`name` AS `powerB_name`,
	`Server_DatacenterDevice`.`redundancy` AS `redundancy`,
	`Server`.`osfamily_id` AS `osfamily_id`,
	`OSFamily_osfamily_id_Typology`.`name` AS `osfamily_name`,
	`Server`.`osversion_id` AS `osversion_id`,
	`OSVersion_osversion_id_Typology`.`name` AS `osversion_name`,
	`Server`.`oslicence_id` AS `oslicence_id`,
	`OSLicence_oslicence_id_Licence`.`name` AS `oslicence_name`,
	`Server`.`cpu` AS `cpu`,
	`Server`.`ram` AS `ram`,
	`Server_FunctionalCI`.`finalclass` AS `finalclass`,
	cast( concat( COALESCE ( `Server_FunctionalCI`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `friendlyname`,
	COALESCE (( `Server_PhysicalDevice`.`status` = 'obsolete' ), 0 ) AS `obsolescence_flag`,
	`Server_FunctionalCI`.`obsolescence_date` AS `obsolescence_date`,
	cast( concat( COALESCE ( `Organization_org_id`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `org_id_friendlyname`,
	COALESCE (( `Organization_org_id`.`status` = 'inactive' ), 0 ) AS `org_id_obsolescence_flag`,
	cast( concat( COALESCE ( `Location_location_id`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `location_id_friendlyname`,
	COALESCE (( `Location_location_id`.`status` = 'inactive' ), 0 ) AS `location_id_obsolescence_flag`,
	cast( concat( COALESCE ( `Brand_brand_id_Typology`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `brand_id_friendlyname`,
	cast( concat( COALESCE ( `Model_model_id_Typology`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `model_id_friendlyname`,
	cast( concat( COALESCE ( `Rack_rack_id_FunctionalCI`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `rack_id_friendlyname`,
	COALESCE (( `Rack_rack_id_PhysicalDevice`.`status` = 'obsolete' ), 0 ) AS `rack_id_obsolescence_flag`,
	cast( concat( COALESCE ( `Enclosure_enclosure_id_FunctionalCI`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `enclosure_id_friendlyname`,
	COALESCE (( `Enclosure_enclosure_id_PhysicalDevice`.`status` = 'obsolete' ), 0 ) AS `enclosure_id_obsolescence_flag`,
	cast( concat( COALESCE ( `PowerConnection_powerA_id_FunctionalCI`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `powerA_id_friendlyname`,
	`PowerConnection_powerA_id_FunctionalCI`.`finalclass` AS `powerA_id_finalclass_recall`,
	COALESCE (( `PowerConnection_powerA_id_PhysicalDevice`.`status` = 'obsolete' ), 0 ) AS `powerA_id_obsolescence_flag`,
	cast( concat( COALESCE ( `PowerConnection_powerB_id_FunctionalCI`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `powerB_id_friendlyname`,
	`PowerConnection_powerB_id_FunctionalCI`.`finalclass` AS `powerB_id_finalclass_recall`,
	COALESCE (( `PowerConnection_powerB_id_PhysicalDevice`.`status` = 'obsolete' ), 0 ) AS `powerB_id_obsolescence_flag`,
	cast( concat( COALESCE ( `OSFamily_osfamily_id_Typology`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `osfamily_id_friendlyname`,
	cast( concat( COALESCE ( `OSVersion_osversion_id_Typology`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `osversion_id_friendlyname`,
	cast( concat( COALESCE ( `OSLicence_oslicence_id_Licence`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `oslicence_id_friendlyname`,
	COALESCE (((
				`OSLicence_oslicence_id_Licence`.`perpetual` = 'no' 
				) 
			AND (( `OSLicence_oslicence_id_Licence`.`end_date` IS NULL ) = 0 ) 
			AND (
			`OSLicence_oslicence_id_Licence`.`end_date` < date_format(( now() - INTERVAL 15 MONTH ), '%Y-%m-%d 00:00:00' ))),
		0 
	) AS `oslicence_id_obsolescence_flag` 
FROM
	((((((
							`server` `Server`
							LEFT JOIN `typology` `OSFamily_osfamily_id_Typology` ON ((
									`Server`.`osfamily_id` = `OSFamily_osfamily_id_Typology`.`id` 
								)))
						LEFT JOIN `typology` `OSVersion_osversion_id_Typology` ON ((
								`Server`.`osversion_id` = `OSVersion_osversion_id_Typology`.`id` 
							)))
					LEFT JOIN `licence` `OSLicence_oslicence_id_Licence` ON ((
							`Server`.`oslicence_id` = `OSLicence_oslicence_id_Licence`.`id` 
						)))
				JOIN ((((
								`datacenterdevice` `Server_DatacenterDevice`
								LEFT JOIN (
									`physicaldevice` `Rack_rack_id_PhysicalDevice`
									JOIN `functionalci` `Rack_rack_id_FunctionalCI` ON ((
											`Rack_rack_id_PhysicalDevice`.`id` = `Rack_rack_id_FunctionalCI`.`id` 
											))) ON ((
										`Server_DatacenterDevice`.`rack_id` = `Rack_rack_id_PhysicalDevice`.`id` 
									)))
							LEFT JOIN (
								`physicaldevice` `Enclosure_enclosure_id_PhysicalDevice`
								JOIN `functionalci` `Enclosure_enclosure_id_FunctionalCI` ON ((
										`Enclosure_enclosure_id_PhysicalDevice`.`id` = `Enclosure_enclosure_id_FunctionalCI`.`id` 
										))) ON ((
									`Server_DatacenterDevice`.`enclosure_id` = `Enclosure_enclosure_id_PhysicalDevice`.`id` 
								)))
						LEFT JOIN (
							`physicaldevice` `PowerConnection_powerA_id_PhysicalDevice`
							JOIN `functionalci` `PowerConnection_powerA_id_FunctionalCI` ON ((
									`PowerConnection_powerA_id_PhysicalDevice`.`id` = `PowerConnection_powerA_id_FunctionalCI`.`id` 
									))) ON ((
								`Server_DatacenterDevice`.`powera_id` = `PowerConnection_powerA_id_PhysicalDevice`.`id` 
							)))
					LEFT JOIN (
						`physicaldevice` `PowerConnection_powerB_id_PhysicalDevice`
						JOIN `functionalci` `PowerConnection_powerB_id_FunctionalCI` ON ((
								`PowerConnection_powerB_id_PhysicalDevice`.`id` = `PowerConnection_powerB_id_FunctionalCI`.`id` 
								))) ON ((
							`Server_DatacenterDevice`.`powerB_id` = `PowerConnection_powerB_id_PhysicalDevice`.`id` 
						))) ON ((
						`Server`.`id` = `Server_DatacenterDevice`.`id` 
					)))
			JOIN (((
						`physicaldevice` `Server_PhysicalDevice`
						LEFT JOIN `location` `Location_location_id` ON ((
								`Server_PhysicalDevice`.`location_id` = `Location_location_id`.`id` 
							)))
					LEFT JOIN `typology` `Brand_brand_id_Typology` ON ((
							`Server_PhysicalDevice`.`brand_id` = `Brand_brand_id_Typology`.`id` 
						)))
				LEFT JOIN `typology` `Model_model_id_Typology` ON ((
						`Server_PhysicalDevice`.`model_id` = `Model_model_id_Typology`.`id` 
						))) ON ((
					`Server`.`id` = `Server_PhysicalDevice`.`id` 
				)))
		JOIN (
			`functionalci` `Server_FunctionalCI`
			JOIN `organization` `Organization_org_id` ON ((
					`Server_FunctionalCI`.`org_id` = `Organization_org_id`.`id` 
					))) ON ((
				`Server`.`id` = `Server_FunctionalCI`.`id` 
			))) 
WHERE
	((
			0 <> COALESCE (( `Brand_brand_id_Typology`.`finalclass` = 'Brand' ), 1 )) 
		AND (
		0 <> COALESCE (( `Model_model_id_Typology`.`finalclass` = 'Model' ), 1 )) 
		AND (
		0 <> COALESCE (( `Rack_rack_id_PhysicalDevice`.`finalclass` = 'Rack' ), 1 )) 
		AND (
		0 <> COALESCE (( `Enclosure_enclosure_id_PhysicalDevice`.`finalclass` = 'Enclosure' ), 1 )) 
		AND (
		0 <> COALESCE (( `PowerConnection_powerA_id_PhysicalDevice`.`finalclass` IN ( 'PowerSource', 'PDU', 'PowerConnection' )), 1 )) 
		AND (
		0 <> COALESCE (( `PowerConnection_powerB_id_PhysicalDevice`.`finalclass` IN ( 'PowerSource', 'PDU', 'PowerConnection' )), 1 )) 
		AND (
		0 <> COALESCE (( `OSFamily_osfamily_id_Typology`.`finalclass` = 'OSFamily' ), 1 )) 
		AND (
		0 <> COALESCE (( `OSVersion_osversion_id_Typology`.`finalclass` = 'OSVersion' ), 1 )) 
	AND (
	0 <> COALESCE (( `OSLicence_oslicence_id_Licence`.`finalclass` = 'OSLicence' ), 1 )))
```

