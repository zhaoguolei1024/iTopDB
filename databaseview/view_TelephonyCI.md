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
select distinct `TelephonyCI`.`id` AS `id`,`TelephonyCI_FunctionalCI`.`name` AS `name`,`TelephonyCI_FunctionalCI`.`description` AS `description`,`TelephonyCI_FunctionalCI`.`org_id` AS `org_id`,`Organization_org_id`.`name` AS `organization_name`,`TelephonyCI_FunctionalCI`.`business_criticity` AS `business_criticity`,`TelephonyCI_FunctionalCI`.`move2production` AS `move2production`,`TelephonyCI_PhysicalDevice`.`serialnumber` AS `serialnumber`,`TelephonyCI_PhysicalDevice`.`location_id` AS `location_id`,`Location_location_id`.`name` AS `location_name`,`TelephonyCI_PhysicalDevice`.`status` AS `status`,`TelephonyCI_PhysicalDevice`.`brand_id` AS `brand_id`,`Brand_brand_id_Typology`.`name` AS `brand_name`,`TelephonyCI_PhysicalDevice`.`model_id` AS `model_id`,`Model_model_id_Typology`.`name` AS `model_name`,`TelephonyCI_PhysicalDevice`.`asset_number` AS `asset_number`,`TelephonyCI_PhysicalDevice`.`purchase_date` AS `purchase_date`,`TelephonyCI_PhysicalDevice`.`end_of_warranty` AS `end_of_warranty`,`TelephonyCI`.`phonenumber` AS `phonenumber`,`TelephonyCI_FunctionalCI`.`finalclass` AS `finalclass`,cast(concat(coalesce(`TelephonyCI_FunctionalCI`.`name`,'')) as char charset utf8mb4) AS `friendlyname`,coalesce((`TelephonyCI_PhysicalDevice`.`status` = 'obsolete'),0) AS `obsolescence_flag`,`TelephonyCI_FunctionalCI`.`obsolescence_date` AS `obsolescence_date`,cast(concat(coalesce(`Organization_org_id`.`name`,'')) as char charset utf8mb4) AS `org_id_friendlyname`,coalesce((`Organization_org_id`.`status` = 'inactive'),0) AS `org_id_obsolescence_flag`,cast(concat(coalesce(`Location_location_id`.`name`,'')) as char charset utf8mb4) AS `location_id_friendlyname`,coalesce((`Location_location_id`.`status` = 'inactive'),0) AS `location_id_obsolescence_flag`,cast(concat(coalesce(`Brand_brand_id_Typology`.`name`,'')) as char charset utf8mb4) AS `brand_id_friendlyname`,cast(concat(coalesce(`Model_model_id_Typology`.`name`,'')) as char charset utf8mb4) AS `model_id_friendlyname` from ((`telephonyci` `TelephonyCI` join (((`physicaldevice` `TelephonyCI_PhysicalDevice` left join `location` `Location_location_id` on((`TelephonyCI_PhysicalDevice`.`location_id` = `Location_location_id`.`id`))) left join `typology` `Brand_brand_id_Typology` on((`TelephonyCI_PhysicalDevice`.`brand_id` = `Brand_brand_id_Typology`.`id`))) left join `typology` `Model_model_id_Typology` on((`TelephonyCI_PhysicalDevice`.`model_id` = `Model_model_id_Typology`.`id`))) on((`TelephonyCI`.`id` = `TelephonyCI_PhysicalDevice`.`id`))) join (`functionalci` `TelephonyCI_FunctionalCI` join `organization` `Organization_org_id` on((`TelephonyCI_FunctionalCI`.`org_id` = `Organization_org_id`.`id`))) on((`TelephonyCI`.`id` = `TelephonyCI_FunctionalCI`.`id`))) where ((0 <> coalesce((`Brand_brand_id_Typology`.`finalclass` = 'Brand'),1)) and (0 <> coalesce((`Model_model_id_Typology`.`finalclass` = 'Model'),1)))
```

