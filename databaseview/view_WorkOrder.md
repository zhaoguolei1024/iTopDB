| 列                          | 类型                                    | 注释 |
| :-------------------------- | --------------------------------------- | ---- |
| id                          | int [**0**]                             |      |
| name                        | varchar(255) *NULL* []                  |      |
| status                      | enum('closed','open') *NULL* [**open**] |      |
| description                 | text *NULL*                             |      |
| ticket_id                   | int *NULL* [**0**]                      |      |
| ticket_ref                  | varchar(255) *NULL* []                  |      |
| team_id                     | int *NULL* [**0**]                      |      |
| team_name                   | varchar(255) *NULL* []                  |      |
| agent_id                    | int *NULL* [**0**]                      |      |
| agent_email                 | varchar(255) *NULL* []                  |      |
| start_date                  | datetime *NULL*                         |      |
| end_date                    | datetime *NULL*                         |      |
| log                         | longtext *NULL*                         |      |
| friendlyname                | varchar(255) *NULL*                     |      |
| ticket_id_friendlyname      | varchar(255) *NULL*                     |      |
| ticket_id_finalclass_recall | varchar(255) *NULL* [**Ticket**]        |      |
| team_id_friendlyname        | varchar(255) *NULL*                     |      |
| team_id_obsolescence_flag   | int [**0**]                             |      |
| agent_id_friendlyname       | varchar(511) *NULL*                     |      |
| agent_id_obsolescence_flag  | int [**0**]                             |      |
| WorkOrderlog_index          | blob *NULL*                             |      |

```
select distinct `WorkOrder`.`id` AS `id`,`WorkOrder`.`name` AS `name`,`WorkOrder`.`status` AS `status`,`WorkOrder`.`description` AS `description`,`WorkOrder`.`ticket_id` AS `ticket_id`,`Ticket_ticket_id`.`ref` AS `ticket_ref`,`WorkOrder`.`team_id` AS `team_id`,`Team_team_id_Contact`.`email` AS `team_name`,`WorkOrder`.`owner_id` AS `agent_id`,`Person_agent_id_Contact`.`email` AS `agent_email`,`WorkOrder`.`start_date` AS `start_date`,`WorkOrder`.`end_date` AS `end_date`,`WorkOrder`.`log` AS `log`,cast(concat(coalesce(`WorkOrder`.`name`,'')) as char charset utf8mb4) AS `friendlyname`,cast(concat(coalesce(`Ticket_ticket_id`.`ref`,'')) as char charset utf8mb4) AS `ticket_id_friendlyname`,`Ticket_ticket_id`.`finalclass` AS `ticket_id_finalclass_recall`,cast(concat(coalesce(`Team_team_id_Contact`.`name`,'')) as char charset utf8mb4) AS `team_id_friendlyname`,coalesce((`Team_team_id_Contact`.`status` = 'inactive'),0) AS `team_id_obsolescence_flag`,cast(concat(coalesce(`Person_agent_id`.`first_name`,''),coalesce(' ',''),coalesce(`Person_agent_id_Contact`.`name`,'')) as char charset utf8mb4) AS `agent_id_friendlyname`,coalesce((`Person_agent_id_Contact`.`status` = 'inactive'),0) AS `agent_id_obsolescence_flag`,`WorkOrder`.`log_index` AS `WorkOrderlog_index` from (((`workorder` `WorkOrder` join `ticket` `Ticket_ticket_id` on((`WorkOrder`.`ticket_id` = `Ticket_ticket_id`.`id`))) join `contact` `Team_team_id_Contact` on((`WorkOrder`.`team_id` = `Team_team_id_Contact`.`id`))) left join (`person` `Person_agent_id` join `contact` `Person_agent_id_Contact` on((`Person_agent_id`.`id` = `Person_agent_id_Contact`.`id`))) on((`WorkOrder`.`owner_id` = `Person_agent_id`.`id`))) where (0 <> coalesce((`Team_team_id_Contact`.`finalclass` = 'Team'),1))
```

