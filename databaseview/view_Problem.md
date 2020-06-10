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
SELECT DISTINCT
	`Problem`.`id` AS `id`,
	`Problem_Ticket`.`operational_status` AS `operational_status`,
	`Problem_Ticket`.`ref` AS `ref`,
	`Problem_Ticket`.`org_id` AS `org_id`,
	`Organization_org_id`.`name` AS `org_name`,
	`Problem_Ticket`.`caller_id` AS `caller_id`,
	`Person_caller_id_Contact`.`name` AS `caller_name`,
	`Problem_Ticket`.`team_id` AS `team_id`,
	`Team_team_id_Contact`.`email` AS `team_name`,
	`Problem_Ticket`.`agent_id` AS `agent_id`,
	`Person_agent_id_Contact`.`name` AS `agent_name`,
	`Problem_Ticket`.`title` AS `title`,
	`Problem_Ticket`.`description` AS `description`,
	`Problem_Ticket`.`start_date` AS `start_date`,
	`Problem_Ticket`.`end_date` AS `end_date`,
	`Problem_Ticket`.`last_update` AS `last_update`,
	`Problem_Ticket`.`close_date` AS `close_date`,
	`Problem_Ticket`.`private_log` AS `private_log`,
	`Problem`.`status` AS `status`,
	`Problem`.`service_id` AS `service_id`,
	`Service_service_id`.`name` AS `service_name`,
	`Problem`.`servicesubcategory_id` AS `servicesubcategory_id`,
	`ServiceSubcategory_servicesubcategory_id`.`name` AS `servicesubcategory_name`,
	`Problem`.`product` AS `product`,
	`Problem`.`impact` AS `impact`,
	`Problem`.`urgency` AS `urgency`,
	`Problem`.`priority` AS `priority`,
	`Problem`.`related_change_id` AS `related_change_id`,
	`Change_related_change_id_Ticket`.`ref` AS `related_change_ref`,
	`Problem`.`assignment_date` AS `assignment_date`,
	`Problem`.`resolution_date` AS `resolution_date`,
	`Problem_Ticket`.`finalclass` AS `finalclass`,
	cast( concat( COALESCE ( `Problem_Ticket`.`ref`, '' )) AS CHAR charset utf8mb4 ) AS `friendlyname`,
	cast( concat( COALESCE ( `Organization_org_id`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `org_id_friendlyname`,
	COALESCE (( `Organization_org_id`.`status` = 'inactive' ), 0 ) AS `org_id_obsolescence_flag`,
	cast(
		concat(
			COALESCE ( `Person_caller_id`.`first_name`, '' ),
			COALESCE ( ' ', '' ),
		COALESCE ( `Person_caller_id_Contact`.`name`, '' )) AS CHAR charset utf8mb4 
	) AS `caller_id_friendlyname`,
	COALESCE (( `Person_caller_id_Contact`.`status` = 'inactive' ), 0 ) AS `caller_id_obsolescence_flag`,
	cast( concat( COALESCE ( `Team_team_id_Contact`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `team_id_friendlyname`,
	COALESCE (( `Team_team_id_Contact`.`status` = 'inactive' ), 0 ) AS `team_id_obsolescence_flag`,
	cast(
		concat(
			COALESCE ( `Person_agent_id`.`first_name`, '' ),
			COALESCE ( ' ', '' ),
		COALESCE ( `Person_agent_id_Contact`.`name`, '' )) AS CHAR charset utf8mb4 
	) AS `agent_id_friendlyname`,
	COALESCE (( `Person_agent_id_Contact`.`status` = 'inactive' ), 0 ) AS `agent_id_obsolescence_flag`,
	cast( concat( COALESCE ( `Service_service_id`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `service_id_friendlyname`,
	cast( concat( COALESCE ( `ServiceSubcategory_servicesubcategory_id`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `servicesubcategory_id_friendlyname`,
	cast( concat( COALESCE ( `Change_related_change_id_Ticket`.`ref`, '' )) AS CHAR charset utf8mb4 ) AS `related_change_id_friendlyname`,
	`Change_related_change_id_Ticket`.`finalclass` AS `related_change_id_finalclass_recall`,
	`Problem_Ticket`.`description_format` AS `Problemdescription_format`,
	`Problem_Ticket`.`private_log_index` AS `Problemprivate_log_index` 
FROM
	((((
					`ticket_problem` `Problem`
					LEFT JOIN `service` `Service_service_id` ON ((
							`Problem`.`service_id` = `Service_service_id`.`id` 
						)))
				LEFT JOIN `servicesubcategory` `ServiceSubcategory_servicesubcategory_id` ON ((
						`Problem`.`servicesubcategory_id` = `ServiceSubcategory_servicesubcategory_id`.`id` 
					)))
			LEFT JOIN `ticket` `Change_related_change_id_Ticket` ON ((
					`Problem`.`related_change_id` = `Change_related_change_id_Ticket`.`id` 
				)))
		JOIN ((((
						`ticket` `Problem_Ticket`
						JOIN `organization` `Organization_org_id` ON ((
								`Problem_Ticket`.`org_id` = `Organization_org_id`.`id` 
							)))
					LEFT JOIN (
						`person` `Person_caller_id`
						JOIN `contact` `Person_caller_id_Contact` ON ((
								`Person_caller_id`.`id` = `Person_caller_id_Contact`.`id` 
								))) ON ((
							`Problem_Ticket`.`caller_id` = `Person_caller_id`.`id` 
						)))
				LEFT JOIN `contact` `Team_team_id_Contact` ON ((
						`Problem_Ticket`.`team_id` = `Team_team_id_Contact`.`id` 
					)))
			LEFT JOIN (
				`person` `Person_agent_id`
				JOIN `contact` `Person_agent_id_Contact` ON ((
						`Person_agent_id`.`id` = `Person_agent_id_Contact`.`id` 
						))) ON ((
					`Problem_Ticket`.`agent_id` = `Person_agent_id`.`id` 
				))) ON ((
				`Problem`.`id` = `Problem_Ticket`.`id` 
			))) 
WHERE
	((
			0 <> COALESCE (( `Team_team_id_Contact`.`finalclass` = 'Team' ), 1 )) 
	AND (
	0 <> COALESCE (( `Change_related_change_id_Ticket`.`finalclass` IN ( 'RoutineChange', 'ApprovedChange', 'NormalChange', 'EmergencyChange', 'Change' )), 1 )))
```

