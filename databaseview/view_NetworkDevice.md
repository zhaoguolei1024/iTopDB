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
select distinct `NetworkDevice`.`id` AS `id`,`NetworkDevice_FunctionalCI`.`name` AS `name`,`NetworkDevice_FunctionalCI`.`description` AS `description`,`NetworkDevice_FunctionalCI`.`org_id` AS `org_id`,`Organization_org_id`.`name` AS `organization_name`,`NetworkDevice_FunctionalCI`.`business_criticity` AS `business_criticity`,`NetworkDevice_FunctionalCI`.`move2production` AS `move2production`,`NetworkDevice_PhysicalDevice`.`serialnumber` AS `serialnumber`,`NetworkDevice_PhysicalDevice`.`location_id` AS `location_id`,`Location_location_id`.`name` AS `location_name`,`NetworkDevice_PhysicalDevice`.`status` AS `status`,`NetworkDevice_PhysicalDevice`.`brand_id` AS `brand_id`,`Brand_brand_id_Typology`.`name` AS `brand_name`,`NetworkDevice_PhysicalDevice`.`model_id` AS `model_id`,`Model_model_id_Typology`.`name` AS `model_name`,`NetworkDevice_PhysicalDevice`.`asset_number` AS `asset_number`,`NetworkDevice_PhysicalDevice`.`purchase_date` AS `purchase_date`,`NetworkDevice_PhysicalDevice`.`end_of_warranty` AS `end_of_warranty`,`NetworkDevice_DatacenterDevice`.`rack_id` AS `rack_id`,`Rack_rack_id_FunctionalCI`.`name` AS `rack_name`,`NetworkDevice_DatacenterDevice`.`enclosure_id` AS `enclosure_id`,`Enclosure_enclosure_id_FunctionalCI`.`name` AS `enclosure_name`,`NetworkDevice_DatacenterDevice`.`nb_u` AS `nb_u`,`NetworkDevice_DatacenterDevice`.`managementip` AS `managementip`,`NetworkDevice_DatacenterDevice`.`powera_id` AS `powerA_id`,`PowerConnection_powerA_id_FunctionalCI`.`name` AS `powerA_name`,`NetworkDevice_DatacenterDevice`.`powerB_id` AS `powerB_id`,`PowerConnection_powerB_id_FunctionalCI`.`name` AS `powerB_name`,`NetworkDevice_DatacenterDevice`.`redundancy` AS `redundancy`,`NetworkDevice`.`networkdevicetype_id` AS `networkdevicetype_id`,`NetworkDeviceType_networkdevicetype_id_Typology`.`name` AS `networkdevicetype_name`,`NetworkDevice`.`iosversion_id` AS `iosversion_id`,`IOSVersion_iosversion_id_Typology`.`name` AS `iosversion_name`,`NetworkDevice`.`ram` AS `ram`,`NetworkDevice_FunctionalCI`.`finalclass` AS `finalclass`,cast(concat(coalesce(`NetworkDevice_FunctionalCI`.`name`,'')) as char charset utf8mb4) AS `friendlyname`,coalesce((`NetworkDevice_PhysicalDevice`.`status` = 'obsolete'),0) AS `obsolescence_flag`,`NetworkDevice_FunctionalCI`.`obsolescence_date` AS `obsolescence_date`,cast(concat(coalesce(`Organization_org_id`.`name`,'')) as char charset utf8mb4) AS `org_id_friendlyname`,coalesce((`Organization_org_id`.`status` = 'inactive'),0) AS `org_id_obsolescence_flag`,cast(concat(coalesce(`Location_location_id`.`name`,'')) as char charset utf8mb4) AS `location_id_friendlyname`,coalesce((`Location_location_id`.`status` = 'inactive'),0) AS `location_id_obsolescence_flag`,cast(concat(coalesce(`Brand_brand_id_Typology`.`name`,'')) as char charset utf8mb4) AS `brand_id_friendlyname`,cast(concat(coalesce(`Model_model_id_Typology`.`name`,'')) as char charset utf8mb4) AS `model_id_friendlyname`,cast(concat(coalesce(`Rack_rack_id_FunctionalCI`.`name`,'')) as char charset utf8mb4) AS `rack_id_friendlyname`,coalesce((`Rack_rack_id_PhysicalDevice`.`status` = 'obsolete'),0) AS `rack_id_obsolescence_flag`,cast(concat(coalesce(`Enclosure_enclosure_id_FunctionalCI`.`name`,'')) as char charset utf8mb4) AS `enclosure_id_friendlyname`,coalesce((`Enclosure_enclosure_id_PhysicalDevice`.`status` = 'obsolete'),0) AS `enclosure_id_obsolescence_flag`,cast(concat(coalesce(`PowerConnection_powerA_id_FunctionalCI`.`name`,'')) as char charset utf8mb4) AS `powerA_id_friendlyname`,`PowerConnection_powerA_id_FunctionalCI`.`finalclass` AS `powerA_id_finalclass_recall`,coalesce((`PowerConnection_powerA_id_PhysicalDevice`.`status` = 'obsolete'),0) AS `powerA_id_obsolescence_flag`,cast(concat(coalesce(`PowerConnection_powerB_id_FunctionalCI`.`name`,'')) as char charset utf8mb4) AS `powerB_id_friendlyname`,`PowerConnection_powerB_id_FunctionalCI`.`finalclass` AS `powerB_id_finalclass_recall`,coalesce((`PowerConnection_powerB_id_PhysicalDevice`.`status` = 'obsolete'),0) AS `powerB_id_obsolescence_flag`,cast(concat(coalesce(`NetworkDeviceType_networkdevicetype_id_Typology`.`name`,'')) as char charset utf8mb4) AS `networkdevicetype_id_friendlyname`,cast(concat(coalesce(`Brand_brand_id1_Typology`.`name`,''),coalesce(' ',''),coalesce(`IOSVersion_iosversion_id_Typology`.`name`,'')) as char charset utf8mb4) AS `iosversion_id_friendlyname` from (((((`networkdevice` `NetworkDevice` join `typology` `NetworkDeviceType_networkdevicetype_id_Typology` on((`NetworkDevice`.`networkdevicetype_id` = `NetworkDeviceType_networkdevicetype_id_Typology`.`id`))) left join ((`iosversion` `IOSVersion_iosversion_id` join `typology` `Brand_brand_id1_Typology` on((`IOSVersion_iosversion_id`.`brand_id` = `Brand_brand_id1_Typology`.`id`))) join `typology` `IOSVersion_iosversion_id_Typology` on((`IOSVersion_iosversion_id`.`id` = `IOSVersion_iosversion_id_Typology`.`id`))) on((`NetworkDevice`.`iosversion_id` = `IOSVersion_iosversion_id`.`id`))) join ((((`datacenterdevice` `NetworkDevice_DatacenterDevice` left join (`physicaldevice` `Rack_rack_id_PhysicalDevice` join `functionalci` `Rack_rack_id_FunctionalCI` on((`Rack_rack_id_PhysicalDevice`.`id` = `Rack_rack_id_FunctionalCI`.`id`))) on((`NetworkDevice_DatacenterDevice`.`rack_id` = `Rack_rack_id_PhysicalDevice`.`id`))) left join (`physicaldevice` `Enclosure_enclosure_id_PhysicalDevice` join `functionalci` `Enclosure_enclosure_id_FunctionalCI` on((`Enclosure_enclosure_id_PhysicalDevice`.`id` = `Enclosure_enclosure_id_FunctionalCI`.`id`))) on((`NetworkDevice_DatacenterDevice`.`enclosure_id` = `Enclosure_enclosure_id_PhysicalDevice`.`id`))) left join (`physicaldevice` `PowerConnection_powerA_id_PhysicalDevice` join `functionalci` `PowerConnection_powerA_id_FunctionalCI` on((`PowerConnection_powerA_id_PhysicalDevice`.`id` = `PowerConnection_powerA_id_FunctionalCI`.`id`))) on((`NetworkDevice_DatacenterDevice`.`powera_id` = `PowerConnection_powerA_id_PhysicalDevice`.`id`))) left join (`physicaldevice` `PowerConnection_powerB_id_PhysicalDevice` join `functionalci` `PowerConnection_powerB_id_FunctionalCI` on((`PowerConnection_powerB_id_PhysicalDevice`.`id` = `PowerConnection_powerB_id_FunctionalCI`.`id`))) on((`NetworkDevice_DatacenterDevice`.`powerB_id` = `PowerConnection_powerB_id_PhysicalDevice`.`id`))) on((`NetworkDevice`.`id` = `NetworkDevice_DatacenterDevice`.`id`))) join (((`physicaldevice` `NetworkDevice_PhysicalDevice` left join `location` `Location_location_id` on((`NetworkDevice_PhysicalDevice`.`location_id` = `Location_location_id`.`id`))) left join `typology` `Brand_brand_id_Typology` on((`NetworkDevice_PhysicalDevice`.`brand_id` = `Brand_brand_id_Typology`.`id`))) left join `typology` `Model_model_id_Typology` on((`NetworkDevice_PhysicalDevice`.`model_id` = `Model_model_id_Typology`.`id`))) on((`NetworkDevice`.`id` = `NetworkDevice_PhysicalDevice`.`id`))) join (`functionalci` `NetworkDevice_FunctionalCI` join `organization` `Organization_org_id` on((`NetworkDevice_FunctionalCI`.`org_id` = `Organization_org_id`.`id`))) on((`NetworkDevice`.`id` = `NetworkDevice_FunctionalCI`.`id`))) where ((0 <> coalesce((`Brand_brand_id_Typology`.`finalclass` = 'Brand'),1)) and (0 <> coalesce((`Model_model_id_Typology`.`finalclass` = 'Model'),1)) and (0 <> coalesce((`Rack_rack_id_PhysicalDevice`.`finalclass` = 'Rack'),1)) and (0 <> coalesce((`Enclosure_enclosure_id_PhysicalDevice`.`finalclass` = 'Enclosure'),1)) and (0 <> coalesce((`PowerConnection_powerA_id_PhysicalDevice`.`finalclass` in ('PowerSource','PDU','PowerConnection')),1)) and (0 <> coalesce((`PowerConnection_powerB_id_PhysicalDevice`.`finalclass` in ('PowerSource','PDU','PowerConnection')),1)) and (0 <> coalesce((`NetworkDeviceType_networkdevicetype_id_Typology`.`finalclass` = 'NetworkDeviceType'),1)) and (0 <> coalesce((`Brand_brand_id1_Typology`.`finalclass` = 'Brand'),1)))
```
