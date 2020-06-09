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
select distinct `PowerConnection_PhysicalDevice`.`id` AS `id`,`PowerConnection_FunctionalCI`.`name` AS `name`,`PowerConnection_FunctionalCI`.`description` AS `description`,`PowerConnection_FunctionalCI`.`org_id` AS `org_id`,`Organization_org_id`.`name` AS `organization_name`,`PowerConnection_FunctionalCI`.`business_criticity` AS `business_criticity`,`PowerConnection_FunctionalCI`.`move2production` AS `move2production`,`PowerConnection_PhysicalDevice`.`serialnumber` AS `serialnumber`,`PowerConnection_PhysicalDevice`.`location_id` AS `location_id`,`Location_location_id`.`name` AS `location_name`,`PowerConnection_PhysicalDevice`.`status` AS `status`,`PowerConnection_PhysicalDevice`.`brand_id` AS `brand_id`,`Brand_brand_id_Typology`.`name` AS `brand_name`,`PowerConnection_PhysicalDevice`.`model_id` AS `model_id`,`Model_model_id_Typology`.`name` AS `model_name`,`PowerConnection_PhysicalDevice`.`asset_number` AS `asset_number`,`PowerConnection_PhysicalDevice`.`purchase_date` AS `purchase_date`,`PowerConnection_PhysicalDevice`.`end_of_warranty` AS `end_of_warranty`,`PowerConnection_FunctionalCI`.`finalclass` AS `finalclass`,cast(concat(coalesce(`PowerConnection_FunctionalCI`.`name`,'')) as char charset utf8mb4) AS `friendlyname`,coalesce((`PowerConnection_PhysicalDevice`.`status` = 'obsolete'),0) AS `obsolescence_flag`,`PowerConnection_FunctionalCI`.`obsolescence_date` AS `obsolescence_date`,cast(concat(coalesce(`Organization_org_id`.`name`,'')) as char charset utf8mb4) AS `org_id_friendlyname`,coalesce((`Organization_org_id`.`status` = 'inactive'),0) AS `org_id_obsolescence_flag`,cast(concat(coalesce(`Location_location_id`.`name`,'')) as char charset utf8mb4) AS `location_id_friendlyname`,coalesce((`Location_location_id`.`status` = 'inactive'),0) AS `location_id_obsolescence_flag`,cast(concat(coalesce(`Brand_brand_id_Typology`.`name`,'')) as char charset utf8mb4) AS `brand_id_friendlyname`,cast(concat(coalesce(`Model_model_id_Typology`.`name`,'')) as char charset utf8mb4) AS `model_id_friendlyname` from ((((`physicaldevice` `PowerConnection_PhysicalDevice` left join `location` `Location_location_id` on((`PowerConnection_PhysicalDevice`.`location_id` = `Location_location_id`.`id`))) left join `typology` `Brand_brand_id_Typology` on((`PowerConnection_PhysicalDevice`.`brand_id` = `Brand_brand_id_Typology`.`id`))) left join `typology` `Model_model_id_Typology` on((`PowerConnection_PhysicalDevice`.`model_id` = `Model_model_id_Typology`.`id`))) join (`functionalci` `PowerConnection_FunctionalCI` join `organization` `Organization_org_id` on((`PowerConnection_FunctionalCI`.`org_id` = `Organization_org_id`.`id`))) on((`PowerConnection_PhysicalDevice`.`id` = `PowerConnection_FunctionalCI`.`id`))) where ((0 <> coalesce((`Brand_brand_id_Typology`.`finalclass` = 'Brand'),1)) and (0 <> coalesce((`Model_model_id_Typology`.`finalclass` = 'Model'),1)) and (0 <> coalesce((`PowerConnection_PhysicalDevice`.`finalclass` in ('PowerSource','PDU','PowerConnection')),1)))
```

