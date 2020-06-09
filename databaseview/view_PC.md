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
| osfamily_id                   | int *NULL* [**0**]                                           |      |
| osfamily_name                 | varchar(255) *NULL* []                                       |      |
| osversion_id                  | int *NULL* [**0**]                                           |      |
| osversion_name                | varchar(255) *NULL* []                                       |      |
| cpu                           | varchar(255) *NULL* []                                       |      |
| ram                           | varchar(255) *NULL* []                                       |      |
| type                          | enum('desktop','laptop') *NULL*                              |      |
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
| osfamily_id_friendlyname      | varchar(255) *NULL*                                          |      |
| osversion_id_friendlyname     | varchar(255) *NULL*                                          |      |

```
select distinct `PC`.`id` AS `id`,`PC_FunctionalCI`.`name` AS `name`,`PC_FunctionalCI`.`description` AS `description`,`PC_FunctionalCI`.`org_id` AS `org_id`,`Organization_org_id`.`name` AS `organization_name`,`PC_FunctionalCI`.`business_criticity` AS `business_criticity`,`PC_FunctionalCI`.`move2production` AS `move2production`,`PC_PhysicalDevice`.`serialnumber` AS `serialnumber`,`PC_PhysicalDevice`.`location_id` AS `location_id`,`Location_location_id`.`name` AS `location_name`,`PC_PhysicalDevice`.`status` AS `status`,`PC_PhysicalDevice`.`brand_id` AS `brand_id`,`Brand_brand_id_Typology`.`name` AS `brand_name`,`PC_PhysicalDevice`.`model_id` AS `model_id`,`Model_model_id_Typology`.`name` AS `model_name`,`PC_PhysicalDevice`.`asset_number` AS `asset_number`,`PC_PhysicalDevice`.`purchase_date` AS `purchase_date`,`PC_PhysicalDevice`.`end_of_warranty` AS `end_of_warranty`,`PC`.`osfamily_id` AS `osfamily_id`,`OSFamily_osfamily_id_Typology`.`name` AS `osfamily_name`,`PC`.`osversion_id` AS `osversion_id`,`OSVersion_osversion_id_Typology`.`name` AS `osversion_name`,`PC`.`cpu` AS `cpu`,`PC`.`ram` AS `ram`,`PC`.`type` AS `type`,`PC_FunctionalCI`.`finalclass` AS `finalclass`,cast(concat(coalesce(`PC_FunctionalCI`.`name`,'')) as char charset utf8mb4) AS `friendlyname`,coalesce((`PC_PhysicalDevice`.`status` = 'obsolete'),0) AS `obsolescence_flag`,`PC_FunctionalCI`.`obsolescence_date` AS `obsolescence_date`,cast(concat(coalesce(`Organization_org_id`.`name`,'')) as char charset utf8mb4) AS `org_id_friendlyname`,coalesce((`Organization_org_id`.`status` = 'inactive'),0) AS `org_id_obsolescence_flag`,cast(concat(coalesce(`Location_location_id`.`name`,'')) as char charset utf8mb4) AS `location_id_friendlyname`,coalesce((`Location_location_id`.`status` = 'inactive'),0) AS `location_id_obsolescence_flag`,cast(concat(coalesce(`Brand_brand_id_Typology`.`name`,'')) as char charset utf8mb4) AS `brand_id_friendlyname`,cast(concat(coalesce(`Model_model_id_Typology`.`name`,'')) as char charset utf8mb4) AS `model_id_friendlyname`,cast(concat(coalesce(`OSFamily_osfamily_id_Typology`.`name`,'')) as char charset utf8mb4) AS `osfamily_id_friendlyname`,cast(concat(coalesce(`OSVersion_osversion_id_Typology`.`name`,'')) as char charset utf8mb4) AS `osversion_id_friendlyname` from ((((`pc` `PC` left join `typology` `OSFamily_osfamily_id_Typology` on((`PC`.`osfamily_id` = `OSFamily_osfamily_id_Typology`.`id`))) left join `typology` `OSVersion_osversion_id_Typology` on((`PC`.`osversion_id` = `OSVersion_osversion_id_Typology`.`id`))) join (((`physicaldevice` `PC_PhysicalDevice` left join `location` `Location_location_id` on((`PC_PhysicalDevice`.`location_id` = `Location_location_id`.`id`))) left join `typology` `Brand_brand_id_Typology` on((`PC_PhysicalDevice`.`brand_id` = `Brand_brand_id_Typology`.`id`))) left join `typology` `Model_model_id_Typology` on((`PC_PhysicalDevice`.`model_id` = `Model_model_id_Typology`.`id`))) on((`PC`.`id` = `PC_PhysicalDevice`.`id`))) join (`functionalci` `PC_FunctionalCI` join `organization` `Organization_org_id` on((`PC_FunctionalCI`.`org_id` = `Organization_org_id`.`id`))) on((`PC`.`id` = `PC_FunctionalCI`.`id`))) where ((0 <> coalesce((`Brand_brand_id_Typology`.`finalclass` = 'Brand'),1)) and (0 <> coalesce((`Model_model_id_Typology`.`finalclass` = 'Model'),1)) and (0 <> coalesce((`OSFamily_osfamily_id_Typology`.`finalclass` = 'OSFamily'),1)) and (0 <> coalesce((`OSVersion_osversion_id_Typology`.`finalclass` = 'OSVersion'),1)))
```

