| 列                            | 类型                                                         | 注释 |
| :---------------------------- | ------------------------------------------------------------ | ---- |
| id                            | int [**0**]                                                  |      |
| name                          | varchar(255) *NULL* []                                       |      |
| description                   | text *NULL*                                                  |      |
| org_id                        | int *NULL* [**0**]                                           |      |
| organization_name             | varchar(255) *NULL* []                                       |      |
| business_criticity            | enum('high','low','medium') *NULL* [**low**]                 |      |
| move2production               | date *NULL*                                                  |      |
| serialnumber                  | varchar(255) *NULL* []                                       |      |
| location_id                   | int *NULL* [**0**]                                           |      |
| location_name                 | varchar(255) *NULL* []                                       |      |
| status                        | enum('implementation','obsolete','production','stock') *NULL* [**production**] |      |
| brand_id                      | int *NULL* [**0**]                                           |      |
| brand_name                    | varchar(255) *NULL* []                                       |      |
| model_id                      | int *NULL* [**0**]                                           |      |
| model_name                    | varchar(255) *NULL* []                                       |      |
| asset_number                  | varchar(255) *NULL* []                                       |      |
| purchase_date                 | date *NULL*                                                  |      |
| end_of_warranty               | date *NULL*                                                  |      |
| phonenumber                   | varchar(255) *NULL* []                                       |      |
| imei                          | varchar(255) *NULL* []                                       |      |
| hw_pin                        | varchar(255) *NULL* []                                       |      |
| finalclass                    | varchar(255) *NULL* [**FunctionalCI**]                       |      |
| friendlyname                  | varchar(255) *NULL*                                          |      |
| obsolescence_flag             | int [**0**]                                                  |      |
| obsolescence_date             | date *NULL*                                                  |      |
| org_id_friendlyname           | varchar(255) *NULL*                                          |      |
| org_id_obsolescence_flag      | int [**0**]                                                  |      |
| location_id_friendlyname      | varchar(255) *NULL*                                          |      |
| location_id_obsolescence_flag | int [**0**]                                                  |      |
| brand_id_friendlyname         | varchar(255) *NULL*                                          |      |
| model_id_friendlyname         | varchar(255) *NULL*                                          |      |

```
SELECT DISTINCT
	`MobilePhone`.`id` AS `id`,
	`MobilePhone_FunctionalCI`.`name` AS `name`,
	`MobilePhone_FunctionalCI`.`description` AS `description`,
	`MobilePhone_FunctionalCI`.`org_id` AS `org_id`,
	`Organization_org_id`.`name` AS `organization_name`,
	`MobilePhone_FunctionalCI`.`business_criticity` AS `business_criticity`,
	`MobilePhone_FunctionalCI`.`move2production` AS `move2production`,
	`MobilePhone_PhysicalDevice`.`serialnumber` AS `serialnumber`,
	`MobilePhone_PhysicalDevice`.`location_id` AS `location_id`,
	`Location_location_id`.`name` AS `location_name`,
	`MobilePhone_PhysicalDevice`.`status` AS `status`,
	`MobilePhone_PhysicalDevice`.`brand_id` AS `brand_id`,
	`Brand_brand_id_Typology`.`name` AS `brand_name`,
	`MobilePhone_PhysicalDevice`.`model_id` AS `model_id`,
	`Model_model_id_Typology`.`name` AS `model_name`,
	`MobilePhone_PhysicalDevice`.`asset_number` AS `asset_number`,
	`MobilePhone_PhysicalDevice`.`purchase_date` AS `purchase_date`,
	`MobilePhone_PhysicalDevice`.`end_of_warranty` AS `end_of_warranty`,
	`MobilePhone_TelephonyCI`.`phonenumber` AS `phonenumber`,
	`MobilePhone`.`imei` AS `imei`,
	`MobilePhone`.`hw_pin` AS `hw_pin`,
	`MobilePhone_FunctionalCI`.`finalclass` AS `finalclass`,
	cast( concat( COALESCE ( `MobilePhone_FunctionalCI`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `friendlyname`,
	COALESCE (( `MobilePhone_PhysicalDevice`.`status` = 'obsolete' ), 0 ) AS `obsolescence_flag`,
	`MobilePhone_FunctionalCI`.`obsolescence_date` AS `obsolescence_date`,
	cast( concat( COALESCE ( `Organization_org_id`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `org_id_friendlyname`,
	COALESCE (( `Organization_org_id`.`status` = 'inactive' ), 0 ) AS `org_id_obsolescence_flag`,
	cast( concat( COALESCE ( `Location_location_id`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `location_id_friendlyname`,
	COALESCE (( `Location_location_id`.`status` = 'inactive' ), 0 ) AS `location_id_obsolescence_flag`,
	cast( concat( COALESCE ( `Brand_brand_id_Typology`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `brand_id_friendlyname`,
	cast( concat( COALESCE ( `Model_model_id_Typology`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `model_id_friendlyname` 
FROM
	(((
				`mobilephone` `MobilePhone`
				JOIN `telephonyci` `MobilePhone_TelephonyCI` ON ((
						`MobilePhone`.`id` = `MobilePhone_TelephonyCI`.`id` 
					)))
			JOIN (((
						`physicaldevice` `MobilePhone_PhysicalDevice`
						LEFT JOIN `location` `Location_location_id` ON ((
								`MobilePhone_PhysicalDevice`.`location_id` = `Location_location_id`.`id` 
							)))
					LEFT JOIN `typology` `Brand_brand_id_Typology` ON ((
							`MobilePhone_PhysicalDevice`.`brand_id` = `Brand_brand_id_Typology`.`id` 
						)))
				LEFT JOIN `typology` `Model_model_id_Typology` ON ((
						`MobilePhone_PhysicalDevice`.`model_id` = `Model_model_id_Typology`.`id` 
						))) ON ((
					`MobilePhone`.`id` = `MobilePhone_PhysicalDevice`.`id` 
				)))
		JOIN (
			`functionalci` `MobilePhone_FunctionalCI`
			JOIN `organization` `Organization_org_id` ON ((
					`MobilePhone_FunctionalCI`.`org_id` = `Organization_org_id`.`id` 
					))) ON ((
				`MobilePhone`.`id` = `MobilePhone_FunctionalCI`.`id` 
			))) 
WHERE
	((
			0 <> COALESCE (( `Brand_brand_id_Typology`.`finalclass` = 'Brand' ), 1 )) 
	AND (
	0 <> COALESCE (( `Model_model_id_Typology`.`finalclass` = 'Model' ), 1 )))
```

