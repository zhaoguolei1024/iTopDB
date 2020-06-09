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
select distinct `lnkContactToTicket`.`id` AS `id`,`lnkContactToTicket`.`ticket_id` AS `ticket_id`,`Ticket_ticket_id`.`ref` AS `ticket_ref`,`lnkContactToTicket`.`contact_id` AS `contact_id`,`Contact_contact_id`.`email` AS `contact_email`,`lnkContactToTicket`.`role` AS `role`,`lnkContactToTicket`.`impact_code` AS `role_code`,cast(concat(coalesce(`lnkContactToTicket`.`ticket_id`,''),coalesce(' ',''),coalesce(`lnkContactToTicket`.`contact_id`,'')) as char charset utf8mb4) AS `friendlyname`,cast(concat(coalesce(`Ticket_ticket_id`.`ref`,'')) as char charset utf8mb4) AS `ticket_id_friendlyname`,`Ticket_ticket_id`.`finalclass` AS `ticket_id_finalclass_recall`,if((`Contact_contact_id`.`finalclass` in ('Team','Contact')),cast(concat(coalesce(`Contact_contact_id`.`name`,'')) as char charset utf8mb4),cast(concat(coalesce(`Contact_contact_id_poly_Person`.`first_name`,''),coalesce(' ',''),coalesce(`Contact_contact_id`.`name`,'')) as char charset utf8mb4)) AS `contact_id_friendlyname`,`Contact_contact_id`.`finalclass` AS `contact_id_finalclass_recall`,coalesce((`Contact_contact_id`.`status` = 'inactive'),0) AS `contact_id_obsolescence_flag` from ((`lnkcontacttoticket` `lnkContactToTicket` join `ticket` `Ticket_ticket_id` on((`lnkContactToTicket`.`ticket_id` = `Ticket_ticket_id`.`id`))) join (`contact` `Contact_contact_id` left join `person` `Contact_contact_id_poly_Person` on((`Contact_contact_id`.`id` = `Contact_contact_id_poly_Person`.`id`))) on((`lnkContactToTicket`.`contact_id` = `Contact_contact_id`.`id`))) where (0 <> 1)
```

