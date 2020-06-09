| 列                                  | 类型                                                        | 注释 |
| :---------------------------------- | ----------------------------------------------------------- | ---- |
| id                                  | int [**0**]                                                 |      |
| operational_status                  | enum('closed','ongoing','resolved') *NULL* [**ongoing**]    |      |
| ref                                 | varchar(255) *NULL* []                                      |      |
| org_id                              | int *NULL* [**0**]                                          |      |
| org_name                            | varchar(255) *NULL* []                                      |      |
| caller_id                           | int *NULL* [**0**]                                          |      |
| caller_name                         | varchar(255) *NULL* []                                      |      |
| team_id                             | int *NULL* [**0**]                                          |      |
| team_name                           | varchar(255) *NULL* []                                      |      |
| agent_id                            | int *NULL* [**0**]                                          |      |
| agent_name                          | varchar(255) *NULL* []                                      |      |
| title                               | varchar(255) *NULL* []                                      |      |
| description                         | text *NULL*                                                 |      |
| start_date                          | datetime *NULL*                                             |      |
| end_date                            | datetime *NULL*                                             |      |
| last_update                         | datetime *NULL*                                             |      |
| close_date                          | datetime *NULL*                                             |      |
| private_log                         | longtext *NULL*                                             |      |
| status                              | enum('assigned','closed','new','resolved') *NULL* [**new**] |      |
| service_id                          | int *NULL* [**0**]                                          |      |
| service_name                        | varchar(255) *NULL* []                                      |      |
| servicesubcategory_id               | int *NULL* [**0**]                                          |      |
| servicesubcategory_name             | varchar(255) *NULL* []                                      |      |
| product                             | varchar(255) *NULL* []                                      |      |
| impact                              | enum('1','2','3') *NULL* [**1**]                            |      |
| urgency                             | enum('1','2','3','4') *NULL* [**1**]                        |      |
| priority                            | enum('1','2','3','4') *NULL* [**1**]                        |      |
| related_change_id                   | int *NULL* [**0**]                                          |      |
| related_change_ref                  | varchar(255) *NULL* []                                      |      |
| assignment_date                     | datetime *NULL*                                             |      |
| resolution_date                     | datetime *NULL*                                             |      |
| finalclass                          | varchar(255) *NULL* [**Ticket**]                            |      |
| friendlyname                        | varchar(255) *NULL*                                         |      |
| org_id_friendlyname                 | varchar(255) *NULL*                                         |      |
| org_id_obsolescence_flag            | int [**0**]                                                 |      |
| caller_id_friendlyname              | varchar(511) *NULL*                                         |      |
| caller_id_obsolescence_flag         | int [**0**]                                                 |      |
| team_id_friendlyname                | varchar(255) *NULL*                                         |      |
| team_id_obsolescence_flag           | int [**0**]                                                 |      |
| agent_id_friendlyname               | varchar(511) *NULL*                                         |      |
| agent_id_obsolescence_flag          | int [**0**]                                                 |      |
| service_id_friendlyname             | varchar(255) *NULL*                                         |      |
| servicesubcategory_id_friendlyname  | varchar(255) *NULL*                                         |      |
| related_change_id_friendlyname      | varchar(255) *NULL*                                         |      |
| related_change_id_finalclass_recall | varchar(255) *NULL* [**Ticket**]                            |      |
| Problemdescription_format           | enum('text','html') *NULL* [**text**]                       |      |
| Problemprivate_log_index            | blob *NULL*                                                 |      |

```
select distinct `Problem`.`id` AS `id`,`Problem_Ticket`.`operational_status` AS `operational_status`,`Problem_Ticket`.`ref` AS `ref`,`Problem_Ticket`.`org_id` AS `org_id`,`Organization_org_id`.`name` AS `org_name`,`Problem_Ticket`.`caller_id` AS `caller_id`,`Person_caller_id_Contact`.`name` AS `caller_name`,`Problem_Ticket`.`team_id` AS `team_id`,`Team_team_id_Contact`.`email` AS `team_name`,`Problem_Ticket`.`agent_id` AS `agent_id`,`Person_agent_id_Contact`.`name` AS `agent_name`,`Problem_Ticket`.`title` AS `title`,`Problem_Ticket`.`description` AS `description`,`Problem_Ticket`.`start_date` AS `start_date`,`Problem_Ticket`.`end_date` AS `end_date`,`Problem_Ticket`.`last_update` AS `last_update`,`Problem_Ticket`.`close_date` AS `close_date`,`Problem_Ticket`.`private_log` AS `private_log`,`Problem`.`status` AS `status`,`Problem`.`service_id` AS `service_id`,`Service_service_id`.`name` AS `service_name`,`Problem`.`servicesubcategory_id` AS `servicesubcategory_id`,`ServiceSubcategory_servicesubcategory_id`.`name` AS `servicesubcategory_name`,`Problem`.`product` AS `product`,`Problem`.`impact` AS `impact`,`Problem`.`urgency` AS `urgency`,`Problem`.`priority` AS `priority`,`Problem`.`related_change_id` AS `related_change_id`,`Change_related_change_id_Ticket`.`ref` AS `related_change_ref`,`Problem`.`assignment_date` AS `assignment_date`,`Problem`.`resolution_date` AS `resolution_date`,`Problem_Ticket`.`finalclass` AS `finalclass`,cast(concat(coalesce(`Problem_Ticket`.`ref`,'')) as char charset utf8mb4) AS `friendlyname`,cast(concat(coalesce(`Organization_org_id`.`name`,'')) as char charset utf8mb4) AS `org_id_friendlyname`,coalesce((`Organization_org_id`.`status` = 'inactive'),0) AS `org_id_obsolescence_flag`,cast(concat(coalesce(`Person_caller_id`.`first_name`,''),coalesce(' ',''),coalesce(`Person_caller_id_Contact`.`name`,'')) as char charset utf8mb4) AS `caller_id_friendlyname`,coalesce((`Person_caller_id_Contact`.`status` = 'inactive'),0) AS `caller_id_obsolescence_flag`,cast(concat(coalesce(`Team_team_id_Contact`.`name`,'')) as char charset utf8mb4) AS `team_id_friendlyname`,coalesce((`Team_team_id_Contact`.`status` = 'inactive'),0) AS `team_id_obsolescence_flag`,cast(concat(coalesce(`Person_agent_id`.`first_name`,''),coalesce(' ',''),coalesce(`Person_agent_id_Contact`.`name`,'')) as char charset utf8mb4) AS `agent_id_friendlyname`,coalesce((`Person_agent_id_Contact`.`status` = 'inactive'),0) AS `agent_id_obsolescence_flag`,cast(concat(coalesce(`Service_service_id`.`name`,'')) as char charset utf8mb4) AS `service_id_friendlyname`,cast(concat(coalesce(`ServiceSubcategory_servicesubcategory_id`.`name`,'')) as char charset utf8mb4) AS `servicesubcategory_id_friendlyname`,cast(concat(coalesce(`Change_related_change_id_Ticket`.`ref`,'')) as char charset utf8mb4) AS `related_change_id_friendlyname`,`Change_related_change_id_Ticket`.`finalclass` AS `related_change_id_finalclass_recall`,`Problem_Ticket`.`description_format` AS `Problemdescription_format`,`Problem_Ticket`.`private_log_index` AS `Problemprivate_log_index` from ((((`ticket_problem` `Problem` left join `service` `Service_service_id` on((`Problem`.`service_id` = `Service_service_id`.`id`))) left join `servicesubcategory` `ServiceSubcategory_servicesubcategory_id` on((`Problem`.`servicesubcategory_id` = `ServiceSubcategory_servicesubcategory_id`.`id`))) left join `ticket` `Change_related_change_id_Ticket` on((`Problem`.`related_change_id` = `Change_related_change_id_Ticket`.`id`))) join ((((`ticket` `Problem_Ticket` join `organization` `Organization_org_id` on((`Problem_Ticket`.`org_id` = `Organization_org_id`.`id`))) left join (`person` `Person_caller_id` join `contact` `Person_caller_id_Contact` on((`Person_caller_id`.`id` = `Person_caller_id_Contact`.`id`))) on((`Problem_Ticket`.`caller_id` = `Person_caller_id`.`id`))) left join `contact` `Team_team_id_Contact` on((`Problem_Ticket`.`team_id` = `Team_team_id_Contact`.`id`))) left join (`person` `Person_agent_id` join `contact` `Person_agent_id_Contact` on((`Person_agent_id`.`id` = `Person_agent_id_Contact`.`id`))) on((`Problem_Ticket`.`agent_id` = `Person_agent_id`.`id`))) on((`Problem`.`id` = `Problem_Ticket`.`id`))) where ((0 <> coalesce((`Team_team_id_Contact`.`finalclass` = 'Team'),1)) and (0 <> coalesce((`Change_related_change_id_Ticket`.`finalclass` in ('RoutineChange','ApprovedChange','NormalChange','EmergencyChange','Change')),1)))
```

