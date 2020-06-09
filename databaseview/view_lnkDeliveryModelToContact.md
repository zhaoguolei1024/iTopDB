| 列                            | 类型                              | 注释 |
| :---------------------------- | --------------------------------- | ---- |
| id                            | int [**0**]                       |      |
| deliverymodel_id              | int *NULL* [**0**]                |      |
| deliverymodel_name            | varchar(255) *NULL* []            |      |
| contact_id                    | int *NULL* [**0**]                |      |
| contact_name                  | varchar(255) *NULL* []            |      |
| role_id                       | int *NULL* [**0**]                |      |
| role_name                     | varchar(255) *NULL* []            |      |
| friendlyname                  | varchar(23) *NULL*                |      |
| deliverymodel_id_friendlyname | varchar(255) *NULL*               |      |
| contact_id_friendlyname       | varchar(511) *NULL*               |      |
| contact_id_finalclass_recall  | varchar(255) *NULL* [**Contact**] |      |
| contact_id_obsolescence_flag  | int [**0**]                       |      |
| role_id_friendlyname          | varchar(255) *NULL*               |      |

```
select distinct `lnkDeliveryModelToContact`.`id` AS `id`,`lnkDeliveryModelToContact`.`deliverymodel_id` AS `deliverymodel_id`,`DeliveryModel_deliverymodel_id`.`name` AS `deliverymodel_name`,`lnkDeliveryModelToContact`.`contact_id` AS `contact_id`,`Contact_contact_id`.`name` AS `contact_name`,`lnkDeliveryModelToContact`.`role_id` AS `role_id`,`ContactType_role_id_Typology`.`name` AS `role_name`,cast(concat(coalesce(`lnkDeliveryModelToContact`.`deliverymodel_id`,''),coalesce(' ',''),coalesce(`lnkDeliveryModelToContact`.`contact_id`,'')) as char charset utf8mb4) AS `friendlyname`,cast(concat(coalesce(`DeliveryModel_deliverymodel_id`.`name`,'')) as char charset utf8mb4) AS `deliverymodel_id_friendlyname`,if((`Contact_contact_id`.`finalclass` in ('Team','Contact')),cast(concat(coalesce(`Contact_contact_id`.`name`,'')) as char charset utf8mb4),cast(concat(coalesce(`Contact_contact_id_poly_Person`.`first_name`,''),coalesce(' ',''),coalesce(`Contact_contact_id`.`name`,'')) as char charset utf8mb4)) AS `contact_id_friendlyname`,`Contact_contact_id`.`finalclass` AS `contact_id_finalclass_recall`,coalesce((`Contact_contact_id`.`status` = 'inactive'),0) AS `contact_id_obsolescence_flag`,cast(concat(coalesce(`ContactType_role_id_Typology`.`name`,'')) as char charset utf8mb4) AS `role_id_friendlyname` from (((`lnkdeliverymodeltocontact` `lnkDeliveryModelToContact` join `deliverymodel` `DeliveryModel_deliverymodel_id` on((`lnkDeliveryModelToContact`.`deliverymodel_id` = `DeliveryModel_deliverymodel_id`.`id`))) join (`contact` `Contact_contact_id` left join `person` `Contact_contact_id_poly_Person` on((`Contact_contact_id`.`id` = `Contact_contact_id_poly_Person`.`id`))) on((`lnkDeliveryModelToContact`.`contact_id` = `Contact_contact_id`.`id`))) left join `typology` `ContactType_role_id_Typology` on((`lnkDeliveryModelToContact`.`role_id` = `ContactType_role_id_Typology`.`id`))) where (0 <> coalesce((`ContactType_role_id_Typology`.`finalclass` = 'ContactType'),1))
```

