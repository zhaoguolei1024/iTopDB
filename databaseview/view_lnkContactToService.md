| 列                           | 类型                              | 注释 |
| :--------------------------- | --------------------------------- | ---- |
| id                           | int [**0**]                       |      |
| service_id                   | int *NULL* [**0**]                |      |
| service_name                 | varchar(255) *NULL* []            |      |
| contact_id                   | int *NULL* [**0**]                |      |
| contact_name                 | varchar(255) *NULL* []            |      |
| friendlyname                 | varchar(23) *NULL*                |      |
| service_id_friendlyname      | varchar(255) *NULL*               |      |
| contact_id_friendlyname      | varchar(511) *NULL*               |      |
| contact_id_finalclass_recall | varchar(255) *NULL* [**Contact**] |      |
| contact_id_obsolescence_flag | int [**0**]                       |      |

```
SELECT DISTINCT
	`lnkContactToService`.`id` AS `id`,
	`lnkContactToService`.`service_id` AS `service_id`,
	`Service_service_id`.`name` AS `service_name`,
	`lnkContactToService`.`contact_id` AS `contact_id`,
	`Contact_contact_id`.`name` AS `contact_name`,
	cast(
		concat(
			COALESCE ( `lnkContactToService`.`service_id`, '' ),
			COALESCE ( ' ', '' ),
		COALESCE ( `lnkContactToService`.`contact_id`, '' )) AS CHAR charset utf8mb4 
	) AS `friendlyname`,
	cast( concat( COALESCE ( `Service_service_id`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `service_id_friendlyname`,
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
	COALESCE (( `Contact_contact_id`.`status` = 'inactive' ), 0 ) AS `contact_id_obsolescence_flag` 
FROM
	((
			`lnkcontacttoservice` `lnkContactToService`
			JOIN `service` `Service_service_id` ON ((
					`lnkContactToService`.`service_id` = `Service_service_id`.`id` 
				)))
		JOIN (
			`contact` `Contact_contact_id`
			LEFT JOIN `person` `Contact_contact_id_poly_Person` ON ((
					`Contact_contact_id`.`id` = `Contact_contact_id_poly_Person`.`id` 
					))) ON ((
				`lnkContactToService`.`contact_id` = `Contact_contact_id`.`id` 
			))) 
WHERE
	(
	0 <> 1)
```

