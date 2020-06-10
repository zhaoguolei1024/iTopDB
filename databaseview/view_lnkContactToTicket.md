| 列                           | 类型                                                         | 注释 |
| :--------------------------- | ------------------------------------------------------------ | ---- |
| id                           | int [**0**]                                                  |      |
| ticket_id                    | int *NULL* [**0**]                                           |      |
| ticket_ref                   | varchar(255) *NULL* []                                       |      |
| contact_id                   | int *NULL* [**0**]                                           |      |
| contact_email                | varchar(255) *NULL* []                                       |      |
| role                         | varchar(255) *NULL* []                                       |      |
| role_code                    | enum('computed','do_not_notify','manual') *NULL* [**manual**] |      |
| friendlyname                 | varchar(23) *NULL*                                           |      |
| ticket_id_friendlyname       | varchar(255) *NULL*                                          |      |
| ticket_id_finalclass_recall  | varchar(255) *NULL* [**Ticket**]                             |      |
| contact_id_friendlyname      | varchar(511) *NULL*                                          |      |
| contact_id_finalclass_recall | varchar(255) *NULL* [**Contact**]                            |      |
| contact_id_obsolescence_flag | int [**0**]                                                  |      |

```
SELECT DISTINCT
	`lnkContactToTicket`.`id` AS `id`,
	`lnkContactToTicket`.`ticket_id` AS `ticket_id`,
	`Ticket_ticket_id`.`ref` AS `ticket_ref`,
	`lnkContactToTicket`.`contact_id` AS `contact_id`,
	`Contact_contact_id`.`email` AS `contact_email`,
	`lnkContactToTicket`.`role` AS `role`,
	`lnkContactToTicket`.`impact_code` AS `role_code`,
	cast(
		concat(
			COALESCE ( `lnkContactToTicket`.`ticket_id`, '' ),
			COALESCE ( ' ', '' ),
		COALESCE ( `lnkContactToTicket`.`contact_id`, '' )) AS CHAR charset utf8mb4 
	) AS `friendlyname`,
	cast( concat( COALESCE ( `Ticket_ticket_id`.`ref`, '' )) AS CHAR charset utf8mb4 ) AS `ticket_id_friendlyname`,
	`Ticket_ticket_id`.`finalclass` AS `ticket_id_finalclass_recall`,
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
			`lnkcontacttoticket` `lnkContactToTicket`
			JOIN `ticket` `Ticket_ticket_id` ON ((
					`lnkContactToTicket`.`ticket_id` = `Ticket_ticket_id`.`id` 
				)))
		JOIN (
			`contact` `Contact_contact_id`
			LEFT JOIN `person` `Contact_contact_id_poly_Person` ON ((
					`Contact_contact_id`.`id` = `Contact_contact_id_poly_Person`.`id` 
					))) ON ((
				`lnkContactToTicket`.`contact_id` = `Contact_contact_id`.`id` 
			))) 
WHERE
	(
	0 <> 1)
```

