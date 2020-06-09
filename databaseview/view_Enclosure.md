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
| rack_id                       | int *NULL* [**0**]                                           |      |
| rack_name                     | varchar(255) *NULL* []                                       |      |
| nb_u                          | int *NULL*                                                   |      |
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
| rack_id_friendlyname          | varchar(255) *NULL*                                          |      |
| rack_id_obsolescence_flag     | int [**0**]                                                  |      |

```
select distinct `Enclosure`.`id` AS `id`,`Enclosure_FunctionalCI`.`name` AS `name`,`Enclosure_FunctionalCI`.`description` AS `description`,`Enclosure_FunctionalCI`.`org_id` AS `org_id`,`Organization_org_id`.`name` AS `organization_name`,`Enclosure_FunctionalCI`.`business_criticity` AS `business_criticity`,`Enclosure_FunctionalCI`.`move2production` AS `move2production`,`Enclosure_PhysicalDevice`.`serialnumber` AS `serialnumber`,`Enclosure_PhysicalDevice`.`location_id` AS `location_id`,`Location_location_id`.`name` AS `location_name`,`Enclosure_PhysicalDevice`.`status` AS `status`,`Enclosure_PhysicalDevice`.`brand_id` AS `brand_id`,`Brand_brand_id_Typology`.`name` AS `brand_name`,`Enclosure_PhysicalDevice`.`model_id` AS `model_id`,`Model_model_id_Typology`.`name` AS `model_name`,`Enclosure_PhysicalDevice`.`asset_number` AS `asset_number`,`Enclosure_PhysicalDevice`.`purchase_date` AS `purchase_date`,`Enclosure_PhysicalDevice`.`end_of_warranty` AS `end_of_warranty`,`Enclosure`.`rack_id` AS `rack_id`,`Rack_rack_id_FunctionalCI`.`name` AS `rack_name`,`Enclosure`.`nb_u` AS `nb_u`,`Enclosure_FunctionalCI`.`finalclass` AS `finalclass`,cast(concat(coalesce(`Enclosure_FunctionalCI`.`name`,'')) as char charset utf8mb4) AS `friendlyname`,coalesce((`Enclosure_PhysicalDevice`.`status` = 'obsolete'),0) AS `obsolescence_flag`,`Enclosure_FunctionalCI`.`obsolescence_date` AS `obsolescence_date`,cast(concat(coalesce(`Organization_org_id`.`name`,'')) as char charset utf8mb4) AS `org_id_friendlyname`,coalesce((`Organization_org_id`.`status` = 'inactive'),0) AS `org_id_obsolescence_flag`,cast(concat(coalesce(`Location_location_id`.`name`,'')) as char charset utf8mb4) AS `location_id_friendlyname`,coalesce((`Location_location_id`.`status` = 'inactive'),0) AS `location_id_obsolescence_flag`,cast(concat(coalesce(`Brand_brand_id_Typology`.`name`,'')) as char charset utf8mb4) AS `brand_id_friendlyname`,cast(concat(coalesce(`Model_model_id_Typology`.`name`,'')) as char charset utf8mb4) AS `model_id_friendlyname`,cast(concat(coalesce(`Rack_rack_id_FunctionalCI`.`name`,'')) as char charset utf8mb4) AS `rack_id_friendlyname`,coalesce((`Rack_rack_id_PhysicalDevice`.`status` = 'obsolete'),0) AS `rack_id_obsolescence_flag` from (((`enclosure` `Enclosure` join (`physicaldevice` `Rack_rack_id_PhysicalDevice` join `functionalci` `Rack_rack_id_FunctionalCI` on((`Rack_rack_id_PhysicalDevice`.`id` = `Rack_rack_id_FunctionalCI`.`id`))) on((`Enclosure`.`rack_id` = `Rack_rack_id_PhysicalDevice`.`id`))) join (((`physicaldevice` `Enclosure_PhysicalDevice` left join `location` `Location_location_id` on((`Enclosure_PhysicalDevice`.`location_id` = `Location_location_id`.`id`))) left join `typology` `Brand_brand_id_Typology` on((`Enclosure_PhysicalDevice`.`brand_id` = `Brand_brand_id_Typology`.`id`))) left join `typology` `Model_model_id_Typology` on((`Enclosure_PhysicalDevice`.`model_id` = `Model_model_id_Typology`.`id`))) on((`Enclosure`.`id` = `Enclosure_PhysicalDevice`.`id`))) join (`functionalci` `Enclosure_FunctionalCI` join `organization` `Organization_org_id` on((`Enclosure_FunctionalCI`.`org_id` = `Organization_org_id`.`id`))) on((`Enclosure`.`id` = `Enclosure_FunctionalCI`.`id`))) where ((0 <> coalesce((`Brand_brand_id_Typology`.`finalclass` = 'Brand'),1)) and (0 <> coalesce((`Model_model_id_Typology`.`finalclass` = 'Model'),1)) and (0 <> coalesce((`Rack_rack_id_PhysicalDevice`.`finalclass` = 'Rack'),1)))
```

