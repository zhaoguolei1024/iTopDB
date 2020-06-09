| 列                          | 类型                                                     | 注释 |
| :-------------------------- | -------------------------------------------------------- | ---- |
| id                          | int [**0**]                                              |      |
| operational_status          | enum('closed','ongoing','resolved') *NULL* [**ongoing**] |      |
| ref                         | varchar(255) *NULL* []                                   |      |
| org_id                      | int *NULL* [**0**]                                       |      |
| org_name                    | varchar(255) *NULL* []                                   |      |
| caller_id                   | int *NULL* [**0**]                                       |      |
| caller_name                 | varchar(255) *NULL* []                                   |      |
| team_id                     | int *NULL* [**0**]                                       |      |
| team_name                   | varchar(255) *NULL* []                                   |      |
| agent_id                    | int *NULL* [**0**]                                       |      |
| agent_name                  | varchar(255) *NULL* []                                   |      |
| title                       | varchar(255) *NULL* []                                   |      |
| description                 | text *NULL*                                              |      |
| start_date                  | datetime *NULL*                                          |      |
| end_date                    | datetime *NULL*                                          |      |
| last_update                 | datetime *NULL*                                          |      |
| close_date                  | datetime *NULL*                                          |      |
| private_log                 | longtext *NULL*                                          |      |
| finalclass                  | varchar(255) *NULL* [**Ticket**]                         |      |
| friendlyname                | varchar(255) *NULL*                                      |      |
| org_id_friendlyname         | varchar(255) *NULL*                                      |      |
| org_id_obsolescence_flag    | int [**0**]                                              |      |
| caller_id_friendlyname      | varchar(511) *NULL*                                      |      |
| caller_id_obsolescence_flag | int [**0**]                                              |      |
| team_id_friendlyname        | varchar(255) *NULL*                                      |      |
| team_id_obsolescence_flag   | int [**0**]                                              |      |
| agent_id_friendlyname       | varchar(511) *NULL*                                      |      |
| agent_id_obsolescence_flag  | int [**0**]                                              |      |
| Ticketdescription_format    | enum('text','html') *NULL* [**text**]                    |      |
| Ticketprivate_log_index     | blob *NULL*                                              |      |

```
select distinct `Ticket`.`id` AS `id`,`Ticket`.`operational_status` AS `operational_status`,`Ticket`.`ref` AS `ref`,`Ticket`.`org_id` AS `org_id`,`Organization_org_id`.`name` AS `org_name`,`Ticket`.`caller_id` AS `caller_id`,`Person_caller_id_Contact`.`name` AS `caller_name`,`Ticket`.`team_id` AS `team_id`,`Team_team_id_Contact`.`email` AS `team_name`,`Ticket`.`agent_id` AS `agent_id`,`Person_agent_id_Contact`.`name` AS `agent_name`,`Ticket`.`title` AS `title`,`Ticket`.`description` AS `description`,`Ticket`.`start_date` AS `start_date`,`Ticket`.`end_date` AS `end_date`,`Ticket`.`last_update` AS `last_update`,`Ticket`.`close_date` AS `close_date`,`Ticket`.`private_log` AS `private_log`,`Ticket`.`finalclass` AS `finalclass`,cast(concat(coalesce(`Ticket`.`ref`,'')) as char charset utf8mb4) AS `friendlyname`,cast(concat(coalesce(`Organization_org_id`.`name`,'')) as char charset utf8mb4) AS `org_id_friendlyname`,coalesce((`Organization_org_id`.`status` = 'inactive'),0) AS `org_id_obsolescence_flag`,cast(concat(coalesce(`Person_caller_id`.`first_name`,''),coalesce(' ',''),coalesce(`Person_caller_id_Contact`.`name`,'')) as char charset utf8mb4) AS `caller_id_friendlyname`,coalesce((`Person_caller_id_Contact`.`status` = 'inactive'),0) AS `caller_id_obsolescence_flag`,cast(concat(coalesce(`Team_team_id_Contact`.`name`,'')) as char charset utf8mb4) AS `team_id_friendlyname`,coalesce((`Team_team_id_Contact`.`status` = 'inactive'),0) AS `team_id_obsolescence_flag`,cast(concat(coalesce(`Person_agent_id`.`first_name`,''),coalesce(' ',''),coalesce(`Person_agent_id_Contact`.`name`,'')) as char charset utf8mb4) AS `agent_id_friendlyname`,coalesce((`Person_agent_id_Contact`.`status` = 'inactive'),0) AS `agent_id_obsolescence_flag`,`Ticket`.`description_format` AS `Ticketdescription_format`,`Ticket`.`private_log_index` AS `Ticketprivate_log_index` from ((((`ticket` `Ticket` join `organization` `Organization_org_id` on((`Ticket`.`org_id` = `Organization_org_id`.`id`))) left join (`person` `Person_caller_id` join `contact` `Person_caller_id_Contact` on((`Person_caller_id`.`id` = `Person_caller_id_Contact`.`id`))) on((`Ticket`.`caller_id` = `Person_caller_id`.`id`))) left join `contact` `Team_team_id_Contact` on((`Ticket`.`team_id` = `Team_team_id_Contact`.`id`))) left join (`person` `Person_agent_id` join `contact` `Person_agent_id_Contact` on((`Person_agent_id`.`id` = `Person_agent_id_Contact`.`id`))) on((`Ticket`.`agent_id` = `Person_agent_id`.`id`))) where (0 <> coalesce((`Team_team_id_Contact`.`finalclass` = 'Team'),1))
```

