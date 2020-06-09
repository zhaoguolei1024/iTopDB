| 列                              | 类型                                                         | 注释 |
| :------------------------------ | ------------------------------------------------------------ | ---- |
| id                              | int [**0**]                                                  |      |
| name                            | varchar(255) *NULL* []                                       |      |
| description                     | text *NULL*                                                  |      |
| org_id                          | int *NULL* [**0**]                                           |      |
| organization_name               | varchar(255) *NULL* []                                       |      |
| business_criticity              | enum('high','low','medium') *NULL* [**low**]                 |      |
| move2production                 | date *NULL*                                                  |      |
| serialnumber                    | varchar(255) *NULL* []                                       |      |
| location_id                     | int *NULL* [**0**]                                           |      |
| location_name                   | varchar(255) *NULL* []                                       |      |
| status                          | enum('implementation','obsolete','production','stock') *NULL* [**production**] |      |
| brand_id                        | int *NULL* [**0**]                                           |      |
| brand_name                      | varchar(255) *NULL* []                                       |      |
| model_id                        | int *NULL* [**0**]                                           |      |
| model_name                      | varchar(255) *NULL* []                                       |      |
| asset_number                    | varchar(255) *NULL* []                                       |      |
| purchase_date                   | date *NULL*                                                  |      |
| end_of_warranty                 | date *NULL*                                                  |      |
| rack_id                         | int *NULL* [**0**]                                           |      |
| rack_name                       | varchar(255) *NULL* []                                       |      |
| powerstart_id                   | int *NULL* [**0**]                                           |      |
| powerstart_name                 | varchar(255) *NULL* []                                       |      |
| finalclass                      | varchar(255) *NULL* [**FunctionalCI**]                       |      |
| friendlyname                    | varchar(255) *NULL*                                          |      |
| obsolescence_flag               | int [**0**]                                                  |      |
| obsolescence_date               | date *NULL*                                                  |      |
| org_id_friendlyname             | varchar(255) *NULL*                                          |      |
| org_id_obsolescence_flag        | int [**0**]                                                  |      |
| location_id_friendlyname        | varchar(255) *NULL*                                          |      |
| location_id_obsolescence_flag   | int [**0**]                                                  |      |
| brand_id_friendlyname           | varchar(255) *NULL*                                          |      |
| model_id_friendlyname           | varchar(255) *NULL*                                          |      |
| rack_id_friendlyname            | varchar(255) *NULL*                                          |      |
| rack_id_obsolescence_flag       | int [**0**]                                                  |      |
| powerstart_id_friendlyname      | varchar(255) *NULL*                                          |      |
| powerstart_id_finalclass_recall | varchar(255) *NULL* [**FunctionalCI**]                       |      |
| powerstart_id_obsolescence_flag | int [**0**]                                                  |      |

```
select distinct `PDU`.`id` AS `id`,`PDU_FunctionalCI`.`name` AS `name`,`PDU_FunctionalCI`.`description` AS `description`,`PDU_FunctionalCI`.`org_id` AS `org_id`,`Organization_org_id`.`name` AS `organization_name`,`PDU_FunctionalCI`.`business_criticity` AS `business_criticity`,`PDU_FunctionalCI`.`move2production` AS `move2production`,`PDU_PhysicalDevice`.`serialnumber` AS `serialnumber`,`PDU_PhysicalDevice`.`location_id` AS `location_id`,`Location_location_id`.`name` AS `location_name`,`PDU_PhysicalDevice`.`status` AS `status`,`PDU_PhysicalDevice`.`brand_id` AS `brand_id`,`Brand_brand_id_Typology`.`name` AS `brand_name`,`PDU_PhysicalDevice`.`model_id` AS `model_id`,`Model_model_id_Typology`.`name` AS `model_name`,`PDU_PhysicalDevice`.`asset_number` AS `asset_number`,`PDU_PhysicalDevice`.`purchase_date` AS `purchase_date`,`PDU_PhysicalDevice`.`end_of_warranty` AS `end_of_warranty`,`PDU`.`rack_id` AS `rack_id`,`Rack_rack_id_FunctionalCI`.`name` AS `rack_name`,`PDU`.`powerstart_id` AS `powerstart_id`,`PowerConnection_powerstart_id_FunctionalCI`.`name` AS `powerstart_name`,`PDU_FunctionalCI`.`finalclass` AS `finalclass`,cast(concat(coalesce(`PDU_FunctionalCI`.`name`,'')) as char charset utf8mb4) AS `friendlyname`,coalesce((`PDU_PhysicalDevice`.`status` = 'obsolete'),0) AS `obsolescence_flag`,`PDU_FunctionalCI`.`obsolescence_date` AS `obsolescence_date`,cast(concat(coalesce(`Organization_org_id`.`name`,'')) as char charset utf8mb4) AS `org_id_friendlyname`,coalesce((`Organization_org_id`.`status` = 'inactive'),0) AS `org_id_obsolescence_flag`,cast(concat(coalesce(`Location_location_id`.`name`,'')) as char charset utf8mb4) AS `location_id_friendlyname`,coalesce((`Location_location_id`.`status` = 'inactive'),0) AS `location_id_obsolescence_flag`,cast(concat(coalesce(`Brand_brand_id_Typology`.`name`,'')) as char charset utf8mb4) AS `brand_id_friendlyname`,cast(concat(coalesce(`Model_model_id_Typology`.`name`,'')) as char charset utf8mb4) AS `model_id_friendlyname`,cast(concat(coalesce(`Rack_rack_id_FunctionalCI`.`name`,'')) as char charset utf8mb4) AS `rack_id_friendlyname`,coalesce((`Rack_rack_id_PhysicalDevice`.`status` = 'obsolete'),0) AS `rack_id_obsolescence_flag`,cast(concat(coalesce(`PowerConnection_powerstart_id_FunctionalCI`.`name`,'')) as char charset utf8mb4) AS `powerstart_id_friendlyname`,`PowerConnection_powerstart_id_FunctionalCI`.`finalclass` AS `powerstart_id_finalclass_recall`,coalesce((`PowerConnection_powerstart_id_PhysicalDevice`.`status` = 'obsolete'),0) AS `powerstart_id_obsolescence_flag` from ((((`pdu` `PDU` join (`physicaldevice` `Rack_rack_id_PhysicalDevice` join `functionalci` `Rack_rack_id_FunctionalCI` on((`Rack_rack_id_PhysicalDevice`.`id` = `Rack_rack_id_FunctionalCI`.`id`))) on((`PDU`.`rack_id` = `Rack_rack_id_PhysicalDevice`.`id`))) left join (`physicaldevice` `PowerConnection_powerstart_id_PhysicalDevice` join `functionalci` `PowerConnection_powerstart_id_FunctionalCI` on((`PowerConnection_powerstart_id_PhysicalDevice`.`id` = `PowerConnection_powerstart_id_FunctionalCI`.`id`))) on((`PDU`.`powerstart_id` = `PowerConnection_powerstart_id_PhysicalDevice`.`id`))) join (((`physicaldevice` `PDU_PhysicalDevice` left join `location` `Location_location_id` on((`PDU_PhysicalDevice`.`location_id` = `Location_location_id`.`id`))) left join `typology` `Brand_brand_id_Typology` on((`PDU_PhysicalDevice`.`brand_id` = `Brand_brand_id_Typology`.`id`))) left join `typology` `Model_model_id_Typology` on((`PDU_PhysicalDevice`.`model_id` = `Model_model_id_Typology`.`id`))) on((`PDU`.`id` = `PDU_PhysicalDevice`.`id`))) join (`functionalci` `PDU_FunctionalCI` join `organization` `Organization_org_id` on((`PDU_FunctionalCI`.`org_id` = `Organization_org_id`.`id`))) on((`PDU`.`id` = `PDU_FunctionalCI`.`id`))) where ((0 <> coalesce((`Brand_brand_id_Typology`.`finalclass` = 'Brand'),1)) and (0 <> coalesce((`Model_model_id_Typology`.`finalclass` = 'Model'),1)) and (0 <> coalesce((`Rack_rack_id_PhysicalDevice`.`finalclass` = 'Rack'),1)) and (0 <> coalesce((`PowerConnection_powerstart_id_PhysicalDevice`.`finalclass` in ('PowerSource','PDU','PowerConnection')),1)))
```

