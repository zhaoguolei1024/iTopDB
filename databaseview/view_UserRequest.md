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
| status                                | enum('approved','assigned','closed','escalated_tto','escalated_ttr','new','pending','rejected','resolved','waiting_for_approval') *NULL* [**new**] |      |
| request_type                          | enum('service_request') *NULL* [**service_request**]         |      |
| impact                                | enum('1','2','3') *NULL* [**1**]                             |      |
| priority                              | enum('1','2','3','4') *NULL* [**4**]                         |      |
| urgency                               | enum('1','2','3','4') *NULL* [**4**]                         |      |
| origin                                | enum('mail','phone','portal') *NULL* [**phone**]             |      |
| approver_id                           | int *NULL* [**0**]                                           |      |
| approver_email                        | varchar(255) *NULL* []                                       |      |
| service_id                            | int *NULL* [**0**]                                           |      |
| service_name                          | varchar(255) *NULL* []                                       |      |
| servicesubcategory_id                 | int *NULL* [**0**]                                           |      |
| servicesubcategory_name               | varchar(255) *NULL* []                                       |      |
| escalation_flag                       | enum('no','yes') *NULL* [**no**]                             |      |
| escalation_reason                     | varchar(255) *NULL* []                                       |      |
| assignment_date                       | datetime *NULL*                                              |      |
| resolution_date                       | datetime *NULL*                                              |      |
| last_pending_date                     | datetime *NULL*                                              |      |
| cumulatedpending                      | int unsigned *NULL*                                          |      |
| tto                                   | int unsigned *NULL*                                          |      |
| ttr                                   | int unsigned *NULL*                                          |      |
| tto_escalation_deadline               | datetime *NULL*                                              |      |
| sla_tto_passed                        | tinyint unsigned *NULL*                                      |      |
| sla_tto_over                          | int unsigned *NULL*                                          |      |
| ttr_escalation_deadline               | datetime *NULL*                                              |      |
| sla_ttr_passed                        | tinyint unsigned *NULL*                                      |      |
| sla_ttr_over                          | int unsigned *NULL*                                          |      |
| time_spent                            | int unsigned *NULL*                                          |      |
| resolution_code                       | enum('assistance','bug fixed','hardware repair','other','software patch','system update','training') *NULL* [**assistance**] |      |
| solution                              | text *NULL*                                                  |      |
| pending_reason                        | text *NULL*                                                  |      |
| parent_request_id                     | int *NULL* [**0**]                                           |      |
| parent_request_ref                    | varchar(255) *NULL* []                                       |      |
| parent_incident_id                    | int *NULL* [**0**]                                           |      |
| parent_incident_ref                   | varchar(255) *NULL* []                                       |      |
| parent_problem_id                     | int *NULL* [**0**]                                           |      |
| parent_problem_ref                    | varchar(255) *NULL* []                                       |      |
| parent_change_id                      | int *NULL* [**0**]                                           |      |
| parent_change_ref                     | varchar(255) *NULL* []                                       |      |
| public_log                            | longtext *NULL*                                              |      |
| user_satisfaction                     | enum('1','2','3','4') *NULL* [**1**]                         |      |
| user_comment                          | text *NULL*                                                  |      |
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
| approver_id_friendlyname              | varchar(511) *NULL*                                          |      |
| approver_id_obsolescence_flag         | int [**0**]                                                  |      |
| service_id_friendlyname               | varchar(255) *NULL*                                          |      |
| servicesubcategory_id_friendlyname    | varchar(255) *NULL*                                          |      |
| parent_request_id_friendlyname        | varchar(255) *NULL*                                          |      |
| parent_incident_id_friendlyname       | varchar(255) *NULL*                                          |      |
| parent_problem_id_friendlyname        | varchar(255) *NULL*                                          |      |
| parent_change_id_friendlyname         | varchar(255) *NULL*                                          |      |
| parent_change_id_finalclass_recall    | varchar(255) *NULL* [**Ticket**]                             |      |
| UserRequestcumulatedpending_started   | datetime *NULL*                                              |      |
| UserRequestcumulatedpending_laststart | datetime *NULL*                                              |      |
| UserRequestcumulatedpending_stopped   | datetime *NULL*                                              |      |
| UserRequesttto_started                | datetime *NULL*                                              |      |
| UserRequesttto_laststart              | datetime *NULL*                                              |      |
| UserRequesttto_stopped                | datetime *NULL*                                              |      |
| UserRequesttto_75_deadline            | datetime *NULL*                                              |      |
| UserRequesttto_75_passed              | tinyint unsigned *NULL*                                      |      |
| UserRequesttto_75_triggered           | tinyint(1) *NULL*                                            |      |
| UserRequesttto_75_overrun             | int unsigned *NULL*                                          |      |
| UserRequesttto_100_deadline           | datetime *NULL*                                              |      |
| UserRequesttto_100_passed             | tinyint unsigned *NULL*                                      |      |
| UserRequesttto_100_triggered          | tinyint(1) *NULL*                                            |      |
| UserRequesttto_100_overrun            | int unsigned *NULL*                                          |      |
| UserRequestttr_started                | datetime *NULL*                                              |      |
| UserRequestttr_laststart              | datetime *NULL*                                              |      |
| UserRequestttr_stopped                | datetime *NULL*                                              |      |
| UserRequestttr_75_deadline            | datetime *NULL*                                              |      |
| UserRequestttr_75_passed              | tinyint unsigned *NULL*                                      |      |
| UserRequestttr_75_triggered           | tinyint(1) *NULL*                                            |      |
| UserRequestttr_75_overrun             | int unsigned *NULL*                                          |      |
| UserRequestttr_100_deadline           | datetime *NULL*                                              |      |
| UserRequestttr_100_passed             | tinyint unsigned *NULL*                                      |      |
| UserRequestttr_100_triggered          | tinyint(1) *NULL*                                            |      |
| UserRequestttr_100_overrun            | int unsigned *NULL*                                          |      |
| UserRequestpublic_log_index           | blob *NULL*                                                  |      |
| UserRequestdescription_format         | enum('text','html') *NULL* [**text**]                        |      |
| UserRequestprivate_log_index          | blob *NULL*                                                  |      |

```
SELECT DISTINCT
	`UserRequest`.`id` AS `id`,
	`UserRequest_Ticket`.`operational_status` AS `operational_status`,
	`UserRequest_Ticket`.`ref` AS `ref`,
	`UserRequest_Ticket`.`org_id` AS `org_id`,
	`Organization_org_id`.`name` AS `org_name`,
	`UserRequest_Ticket`.`caller_id` AS `caller_id`,
	`Person_caller_id_Contact`.`name` AS `caller_name`,
	`UserRequest_Ticket`.`team_id` AS `team_id`,
	`Team_team_id_Contact`.`email` AS `team_name`,
	`UserRequest_Ticket`.`agent_id` AS `agent_id`,
	`Person_agent_id_Contact`.`name` AS `agent_name`,
	`UserRequest_Ticket`.`title` AS `title`,
	`UserRequest_Ticket`.`description` AS `description`,
	`UserRequest_Ticket`.`start_date` AS `start_date`,
	`UserRequest_Ticket`.`end_date` AS `end_date`,
	`UserRequest_Ticket`.`last_update` AS `last_update`,
	`UserRequest_Ticket`.`close_date` AS `close_date`,
	`UserRequest_Ticket`.`private_log` AS `private_log`,
	`UserRequest`.`status` AS `status`,
	`UserRequest`.`request_type` AS `request_type`,
	`UserRequest`.`impact` AS `impact`,
	`UserRequest`.`priority` AS `priority`,
	`UserRequest`.`urgency` AS `urgency`,
	`UserRequest`.`origin` AS `origin`,
	`UserRequest`.`approver_id` AS `approver_id`,
	`Person_approver_id_Contact`.`email` AS `approver_email`,
	`UserRequest`.`service_id` AS `service_id`,
	`Service_service_id`.`name` AS `service_name`,
	`UserRequest`.`servicesubcategory_id` AS `servicesubcategory_id`,
	`ServiceSubcategory_servicesubcategory_id`.`name` AS `servicesubcategory_name`,
	`UserRequest`.`escalation_flag` AS `escalation_flag`,
	`UserRequest`.`escalation_reason` AS `escalation_reason`,
	`UserRequest`.`assignment_date` AS `assignment_date`,
	`UserRequest`.`resolution_date` AS `resolution_date`,
	`UserRequest`.`last_pending_date` AS `last_pending_date`,
	`UserRequest`.`cumulatedpending_timespent` AS `cumulatedpending`,
	`UserRequest`.`tto_timespent` AS `tto`,
	`UserRequest`.`ttr_timespent` AS `ttr`,
	`UserRequest`.`tto_100_deadline` AS `tto_escalation_deadline`,
	`UserRequest`.`tto_100_passed` AS `sla_tto_passed`,
	`UserRequest`.`tto_100_overrun` AS `sla_tto_over`,
	`UserRequest`.`ttr_100_deadline` AS `ttr_escalation_deadline`,
	`UserRequest`.`ttr_100_passed` AS `sla_ttr_passed`,
	`UserRequest`.`ttr_100_overrun` AS `sla_ttr_over`,
	`UserRequest`.`time_spent` AS `time_spent`,
	`UserRequest`.`resolution_code` AS `resolution_code`,
	`UserRequest`.`solution` AS `solution`,
	`UserRequest`.`pending_reason` AS `pending_reason`,
	`UserRequest`.`parent_request_id` AS `parent_request_id`,
	`UserRequest_parent_request_id_Ticket`.`ref` AS `parent_request_ref`,
	`UserRequest`.`parent_incident_id` AS `parent_incident_id`,
	`Incident_parent_incident_id_Ticket`.`ref` AS `parent_incident_ref`,
	`UserRequest`.`parent_problem_id` AS `parent_problem_id`,
	`Problem_parent_problem_id_Ticket`.`ref` AS `parent_problem_ref`,
	`UserRequest`.`parent_change_id` AS `parent_change_id`,
	`Change_parent_change_id_Ticket`.`ref` AS `parent_change_ref`,
	`UserRequest`.`public_log` AS `public_log`,
	`UserRequest`.`user_satisfaction` AS `user_satisfaction`,
	`UserRequest`.`user_commment` AS `user_comment`,
	`UserRequest_Ticket`.`finalclass` AS `finalclass`,
	cast( concat( COALESCE ( `UserRequest_Ticket`.`ref`, '' )) AS CHAR charset utf8mb4 ) AS `friendlyname`,
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
			COALESCE ( `Person_approver_id`.`first_name`, '' ),
			COALESCE ( ' ', '' ),
		COALESCE ( `Person_approver_id_Contact`.`name`, '' )) AS CHAR charset utf8mb4 
	) AS `approver_id_friendlyname`,
	COALESCE (( `Person_approver_id_Contact`.`status` = 'inactive' ), 0 ) AS `approver_id_obsolescence_flag`,
	cast( concat( COALESCE ( `Service_service_id`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `service_id_friendlyname`,
	cast( concat( COALESCE ( `ServiceSubcategory_servicesubcategory_id`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `servicesubcategory_id_friendlyname`,
	cast( concat( COALESCE ( `UserRequest_parent_request_id_Ticket`.`ref`, '' )) AS CHAR charset utf8mb4 ) AS `parent_request_id_friendlyname`,
	cast( concat( COALESCE ( `Incident_parent_incident_id_Ticket`.`ref`, '' )) AS CHAR charset utf8mb4 ) AS `parent_incident_id_friendlyname`,
	cast( concat( COALESCE ( `Problem_parent_problem_id_Ticket`.`ref`, '' )) AS CHAR charset utf8mb4 ) AS `parent_problem_id_friendlyname`,
	cast( concat( COALESCE ( `Change_parent_change_id_Ticket`.`ref`, '' )) AS CHAR charset utf8mb4 ) AS `parent_change_id_friendlyname`,
	`Change_parent_change_id_Ticket`.`finalclass` AS `parent_change_id_finalclass_recall`,
	`UserRequest`.`cumulatedpending_started` AS `UserRequestcumulatedpending_started`,
	`UserRequest`.`cumulatedpending_laststart` AS `UserRequestcumulatedpending_laststart`,
	`UserRequest`.`cumulatedpending_stopped` AS `UserRequestcumulatedpending_stopped`,
	`UserRequest`.`tto_started` AS `UserRequesttto_started`,
	`UserRequest`.`tto_laststart` AS `UserRequesttto_laststart`,
	`UserRequest`.`tto_stopped` AS `UserRequesttto_stopped`,
	`UserRequest`.`tto_75_deadline` AS `UserRequesttto_75_deadline`,
	`UserRequest`.`tto_75_passed` AS `UserRequesttto_75_passed`,
	`UserRequest`.`tto_75_triggered` AS `UserRequesttto_75_triggered`,
	`UserRequest`.`tto_75_overrun` AS `UserRequesttto_75_overrun`,
	`UserRequest`.`tto_100_deadline` AS `UserRequesttto_100_deadline`,
	`UserRequest`.`tto_100_passed` AS `UserRequesttto_100_passed`,
	`UserRequest`.`tto_100_triggered` AS `UserRequesttto_100_triggered`,
	`UserRequest`.`tto_100_overrun` AS `UserRequesttto_100_overrun`,
	`UserRequest`.`ttr_started` AS `UserRequestttr_started`,
	`UserRequest`.`ttr_laststart` AS `UserRequestttr_laststart`,
	`UserRequest`.`ttr_stopped` AS `UserRequestttr_stopped`,
	`UserRequest`.`ttr_75_deadline` AS `UserRequestttr_75_deadline`,
	`UserRequest`.`ttr_75_passed` AS `UserRequestttr_75_passed`,
	`UserRequest`.`ttr_75_triggered` AS `UserRequestttr_75_triggered`,
	`UserRequest`.`ttr_75_overrun` AS `UserRequestttr_75_overrun`,
	`UserRequest`.`ttr_100_deadline` AS `UserRequestttr_100_deadline`,
	`UserRequest`.`ttr_100_passed` AS `UserRequestttr_100_passed`,
	`UserRequest`.`ttr_100_triggered` AS `UserRequestttr_100_triggered`,
	`UserRequest`.`ttr_100_overrun` AS `UserRequestttr_100_overrun`,
	`UserRequest`.`public_log_index` AS `UserRequestpublic_log_index`,
	`UserRequest_Ticket`.`description_format` AS `UserRequestdescription_format`,
	`UserRequest_Ticket`.`private_log_index` AS `UserRequestprivate_log_index` 
FROM
	((((((((
									`ticket_request` `UserRequest`
									LEFT JOIN (
										`person` `Person_approver_id`
										JOIN `contact` `Person_approver_id_Contact` ON ((
												`Person_approver_id`.`id` = `Person_approver_id_Contact`.`id` 
												))) ON ((
											`UserRequest`.`approver_id` = `Person_approver_id`.`id` 
										)))
								LEFT JOIN `service` `Service_service_id` ON ((
										`UserRequest`.`service_id` = `Service_service_id`.`id` 
									)))
							LEFT JOIN `servicesubcategory` `ServiceSubcategory_servicesubcategory_id` ON ((
									`UserRequest`.`servicesubcategory_id` = `ServiceSubcategory_servicesubcategory_id`.`id` 
								)))
						LEFT JOIN `ticket` `UserRequest_parent_request_id_Ticket` ON ((
								`UserRequest`.`parent_request_id` = `UserRequest_parent_request_id_Ticket`.`id` 
							)))
					LEFT JOIN `ticket` `Incident_parent_incident_id_Ticket` ON ((
							`UserRequest`.`parent_incident_id` = `Incident_parent_incident_id_Ticket`.`id` 
						)))
				LEFT JOIN `ticket` `Problem_parent_problem_id_Ticket` ON ((
						`UserRequest`.`parent_problem_id` = `Problem_parent_problem_id_Ticket`.`id` 
					)))
			LEFT JOIN `ticket` `Change_parent_change_id_Ticket` ON ((
					`UserRequest`.`parent_change_id` = `Change_parent_change_id_Ticket`.`id` 
				)))
		JOIN ((((
						`ticket` `UserRequest_Ticket`
						JOIN `organization` `Organization_org_id` ON ((
								`UserRequest_Ticket`.`org_id` = `Organization_org_id`.`id` 
							)))
					LEFT JOIN (
						`person` `Person_caller_id`
						JOIN `contact` `Person_caller_id_Contact` ON ((
								`Person_caller_id`.`id` = `Person_caller_id_Contact`.`id` 
								))) ON ((
							`UserRequest_Ticket`.`caller_id` = `Person_caller_id`.`id` 
						)))
				LEFT JOIN `contact` `Team_team_id_Contact` ON ((
						`UserRequest_Ticket`.`team_id` = `Team_team_id_Contact`.`id` 
					)))
			LEFT JOIN (
				`person` `Person_agent_id`
				JOIN `contact` `Person_agent_id_Contact` ON ((
						`Person_agent_id`.`id` = `Person_agent_id_Contact`.`id` 
						))) ON ((
					`UserRequest_Ticket`.`agent_id` = `Person_agent_id`.`id` 
				))) ON ((
				`UserRequest`.`id` = `UserRequest_Ticket`.`id` 
			))) 
WHERE
	((
			0 <> COALESCE (( `Team_team_id_Contact`.`finalclass` = 'Team' ), 1 )) 
		AND (
		0 <> COALESCE (( `UserRequest_parent_request_id_Ticket`.`finalclass` = 'UserRequest' ), 1 )) 
		AND (
		0 <> COALESCE (( `Incident_parent_incident_id_Ticket`.`finalclass` = 'Incident' ), 1 )) 
		AND (
		0 <> COALESCE (( `Problem_parent_problem_id_Ticket`.`finalclass` = 'Problem' ), 1 )) 
	AND (
	0 <> COALESCE (( `Change_parent_change_id_Ticket`.`finalclass` IN ( 'RoutineChange', 'ApprovedChange', 'NormalChange', 'EmergencyChange', 'Change' )), 1 )))
```

