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
SELECT DISTINCT
	`lnkDeliveryModelToContact`.`id` AS `id`,
	`lnkDeliveryModelToContact`.`deliverymodel_id` AS `deliverymodel_id`,
	`DeliveryModel_deliverymodel_id`.`name` AS `deliverymodel_name`,
	`lnkDeliveryModelToContact`.`contact_id` AS `contact_id`,
	`Contact_contact_id`.`name` AS `contact_name`,
	`lnkDeliveryModelToContact`.`role_id` AS `role_id`,
	`ContactType_role_id_Typology`.`name` AS `role_name`,
	cast(
		concat(
			COALESCE ( `lnkDeliveryModelToContact`.`deliverymodel_id`, '' ),
			COALESCE ( ' ', '' ),
		COALESCE ( `lnkDeliveryModelToContact`.`contact_id`, '' )) AS CHAR charset utf8mb4 
	) AS `friendlyname`,
	cast( concat( COALESCE ( `DeliveryModel_deliverymodel_id`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `deliverymodel_id_friendlyname`,
IF
	((
			`Contact_contact_id`.`finalclass` IN ( 'Team', 'Contact' )),
		cast( concat( COALESCE ( `Contact_contact_id`.`name`, '' )) AS CHAR charset utf8mb4 ),
		cast(
			concat(
				COALESCE ( `Contact_contact_id_poly_Person`.`first_name`, '' ),
				COALESCE ( ' ', '' ),
			COALESCE ( `Contact_contact_id`.`name`, '' )) AS CHAR charset utf8mb4 
		)) AS `contact_id_friendlyname`,
	`Contact_contact_id`.`finalclass` AS `contact_id_finalclass_recall`,
	COALESCE (( `Contact_contact_id`.`status` = 'inactive' ), 0 ) AS `contact_id_obsolescence_flag`,
	cast( concat( COALESCE ( `ContactType_role_id_Typology`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `role_id_friendlyname` 
FROM
	(((
				`lnkdeliverymodeltocontact` `lnkDeliveryModelToContact`
				JOIN `deliverymodel` `DeliveryModel_deliverymodel_id` ON ((
						`lnkDeliveryModelToContact`.`deliverymodel_id` = `DeliveryModel_deliverymodel_id`.`id` 
					)))
			JOIN (
				`contact` `Contact_contact_id`
				LEFT JOIN `person` `Contact_contact_id_poly_Person` ON ((
						`Contact_contact_id`.`id` = `Contact_contact_id_poly_Person`.`id` 
						))) ON ((
					`lnkDeliveryModelToContact`.`contact_id` = `Contact_contact_id`.`id` 
				)))
		LEFT JOIN `typology` `ContactType_role_id_Typology` ON ((
				`lnkDeliveryModelToContact`.`role_id` = `ContactType_role_id_Typology`.`id` 
			))) 
WHERE
	(
	0 <> COALESCE (( `ContactType_role_id_Typology`.`finalclass` = 'ContactType' ), 1 ))
```

