| 列                                | 类型                                                         | 注释 |
| :-------------------------------- | ------------------------------------------------------------ | ---- |
| id                                | int [**0**]                                                  |      |
| name                              | varchar(255) *NULL* []                                       |      |
| description                       | text *NULL*                                                  |      |
| org_id                            | int *NULL* [**0**]                                           |      |
| organization_name                 | varchar(255) *NULL* []                                       |      |
| business_criticity                | enum('high','low','medium') *NULL* [**low**]                 |      |
| move2production                   | date *NULL*                                                  |      |
| serialnumber                      | varchar(255) *NULL* []                                       |      |
| location_id                       | int *NULL* [**0**]                                           |      |
| location_name                     | varchar(255) *NULL* []                                       |      |
| status                            | enum('implementation','obsolete','production','stock') *NULL* [**production**] |      |
| brand_id                          | int *NULL* [**0**]                                           |      |
| brand_name                        | varchar(255) *NULL* []                                       |      |
| model_id                          | int *NULL* [**0**]                                           |      |
| model_name                        | varchar(255) *NULL* []                                       |      |
| asset_number                      | varchar(255) *NULL* []                                       |      |
| purchase_date                     | date *NULL*                                                  |      |
| end_of_warranty                   | date *NULL*                                                  |      |
| rack_id                           | int *NULL* [**0**]                                           |      |
| rack_name                         | varchar(255) *NULL* []                                       |      |
| enclosure_id                      | int *NULL* [**0**]                                           |      |
| enclosure_name                    | varchar(255) *NULL* []                                       |      |
| nb_u                              | int *NULL*                                                   |      |
| managementip                      | varchar(255) *NULL* []                                       |      |
| powerA_id                         | int *NULL* [**0**]                                           |      |
| powerA_name                       | varchar(255) *NULL* []                                       |      |
| powerB_id                         | int *NULL* [**0**]                                           |      |
| powerB_name                       | varchar(255) *NULL* []                                       |      |
| redundancy                        | varchar(20) *NULL* [**1**]                                   |      |
| networkdevicetype_id              | int *NULL* [**0**]                                           |      |
| networkdevicetype_name            | varchar(255) *NULL* []                                       |      |
| iosversion_id                     | int *NULL* [**0**]                                           |      |
| iosversion_name                   | varchar(255) *NULL* []                                       |      |
| ram                               | varchar(255) *NULL* []                                       |      |
| finalclass                        | varchar(255) *NULL* [**FunctionalCI**]                       |      |
| friendlyname                      | varchar(255) *NULL*                                          |      |
| obsolescence_flag                 | int [**0**]                                                  |      |
| obsolescence_date                 | date *NULL*                                                  |      |
| org_id_friendlyname               | varchar(255) *NULL*                                          |      |
| org_id_obsolescence_flag          | int [**0**]                                                  |      |
| location_id_friendlyname          | varchar(255) *NULL*                                          |      |
| location_id_obsolescence_flag     | int [**0**]                                                  |      |
| brand_id_friendlyname             | varchar(255) *NULL*                                          |      |
| model_id_friendlyname             | varchar(255) *NULL*                                          |      |
| rack_id_friendlyname              | varchar(255) *NULL*                                          |      |
| rack_id_obsolescence_flag         | int [**0**]                                                  |      |
| enclosure_id_friendlyname         | varchar(255) *NULL*                                          |      |
| enclosure_id_obsolescence_flag    | int [**0**]                                                  |      |
| powerA_id_friendlyname            | varchar(255) *NULL*                                          |      |
| powerA_id_finalclass_recall       | varchar(255) *NULL* [**FunctionalCI**]                       |      |
| powerA_id_obsolescence_flag       | int [**0**]                                                  |      |
| powerB_id_friendlyname            | varchar(255) *NULL*                                          |      |
| powerB_id_finalclass_recall       | varchar(255) *NULL* [**FunctionalCI**]                       |      |
| powerB_id_obsolescence_flag       | int [**0**]                                                  |      |
| networkdevicetype_id_friendlyname | varchar(255) *NULL*                                          |      |
| iosversion_id_friendlyname        | varchar(511) *NULL*                                          |      |

```
SELECT DISTINCT
	`NetworkDevice`.`id` AS `id`,
	`NetworkDevice_FunctionalCI`.`name` AS `name`,
	`NetworkDevice_FunctionalCI`.`description` AS `description`,
	`NetworkDevice_FunctionalCI`.`org_id` AS `org_id`,
	`Organization_org_id`.`name` AS `organization_name`,
	`NetworkDevice_FunctionalCI`.`business_criticity` AS `business_criticity`,
	`NetworkDevice_FunctionalCI`.`move2production` AS `move2production`,
	`NetworkDevice_PhysicalDevice`.`serialnumber` AS `serialnumber`,
	`NetworkDevice_PhysicalDevice`.`location_id` AS `location_id`,
	`Location_location_id`.`name` AS `location_name`,
	`NetworkDevice_PhysicalDevice`.`status` AS `status`,
	`NetworkDevice_PhysicalDevice`.`brand_id` AS `brand_id`,
	`Brand_brand_id_Typology`.`name` AS `brand_name`,
	`NetworkDevice_PhysicalDevice`.`model_id` AS `model_id`,
	`Model_model_id_Typology`.`name` AS `model_name`,
	`NetworkDevice_PhysicalDevice`.`asset_number` AS `asset_number`,
	`NetworkDevice_PhysicalDevice`.`purchase_date` AS `purchase_date`,
	`NetworkDevice_PhysicalDevice`.`end_of_warranty` AS `end_of_warranty`,
	`NetworkDevice_DatacenterDevice`.`rack_id` AS `rack_id`,
	`Rack_rack_id_FunctionalCI`.`name` AS `rack_name`,
	`NetworkDevice_DatacenterDevice`.`enclosure_id` AS `enclosure_id`,
	`Enclosure_enclosure_id_FunctionalCI`.`name` AS `enclosure_name`,
	`NetworkDevice_DatacenterDevice`.`nb_u` AS `nb_u`,
	`NetworkDevice_DatacenterDevice`.`managementip` AS `managementip`,
	`NetworkDevice_DatacenterDevice`.`powera_id` AS `powerA_id`,
	`PowerConnection_powerA_id_FunctionalCI`.`name` AS `powerA_name`,
	`NetworkDevice_DatacenterDevice`.`powerB_id` AS `powerB_id`,
	`PowerConnection_powerB_id_FunctionalCI`.`name` AS `powerB_name`,
	`NetworkDevice_DatacenterDevice`.`redundancy` AS `redundancy`,
	`NetworkDevice`.`networkdevicetype_id` AS `networkdevicetype_id`,
	`NetworkDeviceType_networkdevicetype_id_Typology`.`name` AS `networkdevicetype_name`,
	`NetworkDevice`.`iosversion_id` AS `iosversion_id`,
	`IOSVersion_iosversion_id_Typology`.`name` AS `iosversion_name`,
	`NetworkDevice`.`ram` AS `ram`,
	`NetworkDevice_FunctionalCI`.`finalclass` AS `finalclass`,
	cast( concat( COALESCE ( `NetworkDevice_FunctionalCI`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `friendlyname`,
	COALESCE (( `NetworkDevice_PhysicalDevice`.`status` = 'obsolete' ), 0 ) AS `obsolescence_flag`,
	`NetworkDevice_FunctionalCI`.`obsolescence_date` AS `obsolescence_date`,
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
	cast( concat( COALESCE ( `NetworkDeviceType_networkdevicetype_id_Typology`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `networkdevicetype_id_friendlyname`,
	cast(
		concat(
			COALESCE ( `Brand_brand_id1_Typology`.`name`, '' ),
			COALESCE ( ' ', '' ),
		COALESCE ( `IOSVersion_iosversion_id_Typology`.`name`, '' )) AS CHAR charset utf8mb4 
	) AS `iosversion_id_friendlyname` 
FROM
	(((((
						`networkdevice` `NetworkDevice`
						JOIN `typology` `NetworkDeviceType_networkdevicetype_id_Typology` ON ((
								`NetworkDevice`.`networkdevicetype_id` = `NetworkDeviceType_networkdevicetype_id_Typology`.`id` 
							)))
					LEFT JOIN ((
							`iosversion` `IOSVersion_iosversion_id`
							JOIN `typology` `Brand_brand_id1_Typology` ON ((
									`IOSVersion_iosversion_id`.`brand_id` = `Brand_brand_id1_Typology`.`id` 
								)))
						JOIN `typology` `IOSVersion_iosversion_id_Typology` ON ((
								`IOSVersion_iosversion_id`.`id` = `IOSVersion_iosversion_id_Typology`.`id` 
								))) ON ((
							`NetworkDevice`.`iosversion_id` = `IOSVersion_iosversion_id`.`id` 
						)))
				JOIN ((((
								`datacenterdevice` `NetworkDevice_DatacenterDevice`
								LEFT JOIN (
									`physicaldevice` `Rack_rack_id_PhysicalDevice`
									JOIN `functionalci` `Rack_rack_id_FunctionalCI` ON ((
											`Rack_rack_id_PhysicalDevice`.`id` = `Rack_rack_id_FunctionalCI`.`id` 
											))) ON ((
										`NetworkDevice_DatacenterDevice`.`rack_id` = `Rack_rack_id_PhysicalDevice`.`id` 
									)))
							LEFT JOIN (
								`physicaldevice` `Enclosure_enclosure_id_PhysicalDevice`
								JOIN `functionalci` `Enclosure_enclosure_id_FunctionalCI` ON ((
										`Enclosure_enclosure_id_PhysicalDevice`.`id` = `Enclosure_enclosure_id_FunctionalCI`.`id` 
										))) ON ((
									`NetworkDevice_DatacenterDevice`.`enclosure_id` = `Enclosure_enclosure_id_PhysicalDevice`.`id` 
								)))
						LEFT JOIN (
							`physicaldevice` `PowerConnection_powerA_id_PhysicalDevice`
							JOIN `functionalci` `PowerConnection_powerA_id_FunctionalCI` ON ((
									`PowerConnection_powerA_id_PhysicalDevice`.`id` = `PowerConnection_powerA_id_FunctionalCI`.`id` 
									))) ON ((
								`NetworkDevice_DatacenterDevice`.`powera_id` = `PowerConnection_powerA_id_PhysicalDevice`.`id` 
							)))
					LEFT JOIN (
						`physicaldevice` `PowerConnection_powerB_id_PhysicalDevice`
						JOIN `functionalci` `PowerConnection_powerB_id_FunctionalCI` ON ((
								`PowerConnection_powerB_id_PhysicalDevice`.`id` = `PowerConnection_powerB_id_FunctionalCI`.`id` 
								))) ON ((
							`NetworkDevice_DatacenterDevice`.`powerB_id` = `PowerConnection_powerB_id_PhysicalDevice`.`id` 
						))) ON ((
						`NetworkDevice`.`id` = `NetworkDevice_DatacenterDevice`.`id` 
					)))
			JOIN (((
						`physicaldevice` `NetworkDevice_PhysicalDevice`
						LEFT JOIN `location` `Location_location_id` ON ((
								`NetworkDevice_PhysicalDevice`.`location_id` = `Location_location_id`.`id` 
							)))
					LEFT JOIN `typology` `Brand_brand_id_Typology` ON ((
							`NetworkDevice_PhysicalDevice`.`brand_id` = `Brand_brand_id_Typology`.`id` 
						)))
				LEFT JOIN `typology` `Model_model_id_Typology` ON ((
						`NetworkDevice_PhysicalDevice`.`model_id` = `Model_model_id_Typology`.`id` 
						))) ON ((
					`NetworkDevice`.`id` = `NetworkDevice_PhysicalDevice`.`id` 
				)))
		JOIN (
			`functionalci` `NetworkDevice_FunctionalCI`
			JOIN `organization` `Organization_org_id` ON ((
					`NetworkDevice_FunctionalCI`.`org_id` = `Organization_org_id`.`id` 
					))) ON ((
				`NetworkDevice`.`id` = `NetworkDevice_FunctionalCI`.`id` 
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
		0 <> COALESCE (( `NetworkDeviceType_networkdevicetype_id_Typology`.`finalclass` = 'NetworkDeviceType' ), 1 )) 
	AND (
	0 <> COALESCE (( `Brand_brand_id1_Typology`.`finalclass` = 'Brand' ), 1 )))
```

