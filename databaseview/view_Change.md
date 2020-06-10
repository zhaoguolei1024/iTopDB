| 列                                    | 类型                                                         | 注释 |
| :------------------------------------ | ------------------------------------------------------------ | ---- |
| id                                    | int [**0**]                                                  |      |
| operational_status                    | enum('closed','ongoing','resolved') *NULL* [**ongoing**]     |      |
| ref                                   | varchar(255) *NULL* []                                       |      |
| org_id                                | int *NULL* [**0**]                                           |      |
| org_name                              | varchar(255) *NULL* []                                       |      |
| caller_id                             | int *NULL* [**0**]                                           |      |
| caller_name                           | varchar(255) *NULL* []                                       |      |
| team_id                               | int *NULL* [**0**]                                           |      |
| team_name                             | varchar(255) *NULL* []                                       |      |
| agent_id                              | int *NULL* [**0**]                                           |      |
| agent_name                            | varchar(255) *NULL* []                                       |      |
| title                                 | varchar(255) *NULL* []                                       |      |
| description                           | text *NULL*                                                  |      |
| start_date                            | datetime *NULL*                                              |      |
| end_date                              | datetime *NULL*                                              |      |
| last_update                           | datetime *NULL*                                              |      |
| close_date                            | datetime *NULL*                                              |      |
| private_log                           | longtext *NULL*                                              |      |
| status                                | enum('approved','assigned','closed','implemented','monitored','new','notapproved','plannedscheduled','rejected','validated') *NULL* [**new**] |      |
| reason                                | varchar(255) *NULL* []                                       |      |
| requestor_id                          | int *NULL* [**0**]                                           |      |
| requestor_email                       | varchar(255) *NULL* []                                       |      |
| creation_date                         | datetime *NULL*                                              |      |
| impact                                | varchar(255) *NULL* []                                       |      |
| supervisor_group_id                   | int *NULL* [**0**]                                           |      |
| supervisor_group_name                 | varchar(255) *NULL* []                                       |      |
| supervisor_id                         | int *NULL* [**0**]                                           |      |
| supervisor_email                      | varchar(255) *NULL* []                                       |      |
| manager_group_id                      | int *NULL* [**0**]                                           |      |
| manager_group_name                    | varchar(255) *NULL* []                                       |      |
| manager_id                            | int *NULL* [**0**]                                           |      |
| manager_email                         | varchar(255) *NULL* []                                       |      |
| outage                                | enum('no','yes') *NULL* [**no**]                             |      |
| fallback                              | text *NULL*                                                  |      |
| parent_id                             | int *NULL* [**0**]                                           |      |
| parent_name                           | varchar(255) *NULL* []                                       |      |
| finalclass                            | varchar(255) *NULL* [**Ticket**]                             |      |
| friendlyname                          | varchar(255) *NULL*                                          |      |
| org_id_friendlyname                   | varchar(255) *NULL*                                          |      |
| org_id_obsolescence_flag              | int [**0**]                                                  |      |
| caller_id_friendlyname                | varchar(511) *NULL*                                          |      |
| caller_id_obsolescence_flag           | int [**0**]                                                  |      |
| team_id_friendlyname                  | varchar(255) *NULL*                                          |      |
| team_id_obsolescence_flag             | int [**0**]                                                  |      |
| agent_id_friendlyname                 | varchar(511) *NULL*                                          |      |
| agent_id_obsolescence_flag            | int [**0**]                                                  |      |
| requestor_id_friendlyname             | varchar(511) *NULL*                                          |      |
| requestor_id_obsolescence_flag        | int [**0**]                                                  |      |
| supervisor_group_id_friendlyname      | varchar(255) *NULL*                                          |      |
| supervisor_group_id_obsolescence_flag | int [**0**]                                                  |      |
| supervisor_id_friendlyname            | varchar(511) *NULL*                                          |      |
| supervisor_id_obsolescence_flag       | int [**0**]                                                  |      |
| manager_group_id_friendlyname         | varchar(255) *NULL*                                          |      |
| manager_group_id_obsolescence_flag    | int [**0**]                                                  |      |
| manager_id_friendlyname               | varchar(511) *NULL*                                          |      |
| manager_id_obsolescence_flag          | int [**0**]                                                  |      |
| parent_id_friendlyname                | varchar(255) *NULL*                                          |      |
| parent_id_finalclass_recall           | varchar(255) *NULL* [**Ticket**]                             |      |
| Changedescription_format              | enum('text','html') *NULL* [**text**]                        |      |
| Changeprivate_log_index               | blob *NULL*                                                  |      |

```
SELECT DISTINCT
	`Change`.`id` AS `id`,
	`Change_Ticket`.`operational_status` AS `operational_status`,
	`Change_Ticket`.`ref` AS `ref`,
	`Change_Ticket`.`org_id` AS `org_id`,
	`Organization_org_id`.`name` AS `org_name`,
	`Change_Ticket`.`caller_id` AS `caller_id`,
	`Person_caller_id_Contact`.`name` AS `caller_name`,
	`Change_Ticket`.`team_id` AS `team_id`,
	`Team_team_id_Contact`.`email` AS `team_name`,
	`Change_Ticket`.`agent_id` AS `agent_id`,
	`Person_agent_id_Contact`.`name` AS `agent_name`,
	`Change_Ticket`.`title` AS `title`,
	`Change_Ticket`.`description` AS `description`,
	`Change_Ticket`.`start_date` AS `start_date`,
	`Change_Ticket`.`end_date` AS `end_date`,
	`Change_Ticket`.`last_update` AS `last_update`,
	`Change_Ticket`.`close_date` AS `close_date`,
	`Change_Ticket`.`private_log` AS `private_log`,
	`Change`.`status` AS `status`,
	`Change`.`reason` AS `reason`,
	`Change`.`requestor_id` AS `requestor_id`,
	`Person_requestor_id_Contact`.`email` AS `requestor_email`,
	`Change`.`creation_date` AS `creation_date`,
	`Change`.`impact` AS `impact`,
	`Change`.`supervisor_group_id` AS `supervisor_group_id`,
	`Team_supervisor_group_id_Contact`.`name` AS `supervisor_group_name`,
	`Change`.`supervisor_id` AS `supervisor_id`,
	`Person_supervisor_id_Contact`.`email` AS `supervisor_email`,
	`Change`.`manager_group_id` AS `manager_group_id`,
	`Team_manager_group_id_Contact`.`name` AS `manager_group_name`,
	`Change`.`manager_id` AS `manager_id`,
	`Person_manager_id_Contact`.`email` AS `manager_email`,
	`Change`.`outage` AS `outage`,
	`Change`.`fallback` AS `fallback`,
	`Change`.`parent_id` AS `parent_id`,
	`Change_parent_id_Ticket`.`ref` AS `parent_name`,
	`Change_Ticket`.`finalclass` AS `finalclass`,
	cast( concat( COALESCE ( `Change_Ticket`.`ref`, '' )) AS CHAR charset utf8mb4 ) AS `friendlyname`,
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
	cast(
		concat(
			COALESCE ( `Person_requestor_id`.`first_name`, '' ),
			COALESCE ( ' ', '' ),
		COALESCE ( `Person_requestor_id_Contact`.`name`, '' )) AS CHAR charset utf8mb4 
	) AS `requestor_id_friendlyname`,
	COALESCE (( `Person_requestor_id_Contact`.`status` = 'inactive' ), 0 ) AS `requestor_id_obsolescence_flag`,
	cast( concat( COALESCE ( `Team_supervisor_group_id_Contact`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `supervisor_group_id_friendlyname`,
	COALESCE (( `Team_supervisor_group_id_Contact`.`status` = 'inactive' ), 0 ) AS `supervisor_group_id_obsolescence_flag`,
	cast(
		concat(
			COALESCE ( `Person_supervisor_id`.`first_name`, '' ),
			COALESCE ( ' ', '' ),
		COALESCE ( `Person_supervisor_id_Contact`.`name`, '' )) AS CHAR charset utf8mb4 
	) AS `supervisor_id_friendlyname`,
	COALESCE (( `Person_supervisor_id_Contact`.`status` = 'inactive' ), 0 ) AS `supervisor_id_obsolescence_flag`,
	cast( concat( COALESCE ( `Team_manager_group_id_Contact`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `manager_group_id_friendlyname`,
	COALESCE (( `Team_manager_group_id_Contact`.`status` = 'inactive' ), 0 ) AS `manager_group_id_obsolescence_flag`,
	cast(
		concat(
			COALESCE ( `Person_manager_id`.`first_name`, '' ),
			COALESCE ( ' ', '' ),
		COALESCE ( `Person_manager_id_Contact`.`name`, '' )) AS CHAR charset utf8mb4 
	) AS `manager_id_friendlyname`,
	COALESCE (( `Person_manager_id_Contact`.`status` = 'inactive' ), 0 ) AS `manager_id_obsolescence_flag`,
	cast( concat( COALESCE ( `Change_parent_id_Ticket`.`ref`, '' )) AS CHAR charset utf8mb4 ) AS `parent_id_friendlyname`,
	`Change_parent_id_Ticket`.`finalclass` AS `parent_id_finalclass_recall`,
	`Change_Ticket`.`description_format` AS `Changedescription_format`,
	`Change_Ticket`.`private_log_index` AS `Changeprivate_log_index` 
FROM
	(((((((
								`change` `Change`
								LEFT JOIN (
									`person` `Person_requestor_id`
									JOIN `contact` `Person_requestor_id_Contact` ON ((
											`Person_requestor_id`.`id` = `Person_requestor_id_Contact`.`id` 
											))) ON ((
										`Change`.`requestor_id` = `Person_requestor_id`.`id` 
									)))
							LEFT JOIN `contact` `Team_supervisor_group_id_Contact` ON ((
									`Change`.`supervisor_group_id` = `Team_supervisor_group_id_Contact`.`id` 
								)))
						LEFT JOIN (
							`person` `Person_supervisor_id`
							JOIN `contact` `Person_supervisor_id_Contact` ON ((
									`Person_supervisor_id`.`id` = `Person_supervisor_id_Contact`.`id` 
									))) ON ((
								`Change`.`supervisor_id` = `Person_supervisor_id`.`id` 
							)))
					LEFT JOIN `contact` `Team_manager_group_id_Contact` ON ((
							`Change`.`manager_group_id` = `Team_manager_group_id_Contact`.`id` 
						)))
				LEFT JOIN (
					`person` `Person_manager_id`
					JOIN `contact` `Person_manager_id_Contact` ON ((
							`Person_manager_id`.`id` = `Person_manager_id_Contact`.`id` 
							))) ON ((
						`Change`.`manager_id` = `Person_manager_id`.`id` 
					)))
			LEFT JOIN `ticket` `Change_parent_id_Ticket` ON ((
					`Change`.`parent_id` = `Change_parent_id_Ticket`.`id` 
				)))
		JOIN ((((
						`ticket` `Change_Ticket`
						JOIN `organization` `Organization_org_id` ON ((
								`Change_Ticket`.`org_id` = `Organization_org_id`.`id` 
							)))
					LEFT JOIN (
						`person` `Person_caller_id`
						JOIN `contact` `Person_caller_id_Contact` ON ((
								`Person_caller_id`.`id` = `Person_caller_id_Contact`.`id` 
								))) ON ((
							`Change_Ticket`.`caller_id` = `Person_caller_id`.`id` 
						)))
				LEFT JOIN `contact` `Team_team_id_Contact` ON ((
						`Change_Ticket`.`team_id` = `Team_team_id_Contact`.`id` 
					)))
			LEFT JOIN (
				`person` `Person_agent_id`
				JOIN `contact` `Person_agent_id_Contact` ON ((
						`Person_agent_id`.`id` = `Person_agent_id_Contact`.`id` 
						))) ON ((
					`Change_Ticket`.`agent_id` = `Person_agent_id`.`id` 
				))) ON ((
				`Change`.`id` = `Change_Ticket`.`id` 
			))) 
WHERE
	((
			0 <> COALESCE (( `Team_team_id_Contact`.`finalclass` = 'Team' ), 1 )) 
		AND (
		0 <> COALESCE (( `Team_supervisor_group_id_Contact`.`finalclass` = 'Team' ), 1 )) 
		AND (
		0 <> COALESCE (( `Team_manager_group_id_Contact`.`finalclass` = 'Team' ), 1 )) 
	AND (
	0 <> COALESCE (( `Change_parent_id_Ticket`.`finalclass` IN ( 'RoutineChange', 'ApprovedChange', 'NormalChange', 'EmergencyChange', 'Change' )), 1 )))
```

