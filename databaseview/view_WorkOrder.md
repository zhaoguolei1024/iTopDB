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
SELECT DISTINCT
	`WorkOrder`.`id` AS `id`,
	`WorkOrder`.`name` AS `name`,
	`WorkOrder`.`status` AS `status`,
	`WorkOrder`.`description` AS `description`,
	`WorkOrder`.`ticket_id` AS `ticket_id`,
	`Ticket_ticket_id`.`ref` AS `ticket_ref`,
	`WorkOrder`.`team_id` AS `team_id`,
	`Team_team_id_Contact`.`email` AS `team_name`,
	`WorkOrder`.`owner_id` AS `agent_id`,
	`Person_agent_id_Contact`.`email` AS `agent_email`,
	`WorkOrder`.`start_date` AS `start_date`,
	`WorkOrder`.`end_date` AS `end_date`,
	`WorkOrder`.`log` AS `log`,
	cast( concat( COALESCE ( `WorkOrder`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `friendlyname`,
	cast( concat( COALESCE ( `Ticket_ticket_id`.`ref`, '' )) AS CHAR charset utf8mb4 ) AS `ticket_id_friendlyname`,
	`Ticket_ticket_id`.`finalclass` AS `ticket_id_finalclass_recall`,
	cast( concat( COALESCE ( `Team_team_id_Contact`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `team_id_friendlyname`,
	COALESCE (( `Team_team_id_Contact`.`status` = 'inactive' ), 0 ) AS `team_id_obsolescence_flag`,
	cast(
		concat(
			COALESCE ( `Person_agent_id`.`first_name`, '' ),
			COALESCE ( ' ', '' ),
		COALESCE ( `Person_agent_id_Contact`.`name`, '' )) AS CHAR charset utf8mb4 
	) AS `agent_id_friendlyname`,
	COALESCE (( `Person_agent_id_Contact`.`status` = 'inactive' ), 0 ) AS `agent_id_obsolescence_flag`,
	`WorkOrder`.`log_index` AS `WorkOrderlog_index` 
FROM
	(((
				`workorder` `WorkOrder`
				JOIN `ticket` `Ticket_ticket_id` ON ((
						`WorkOrder`.`ticket_id` = `Ticket_ticket_id`.`id` 
					)))
			JOIN `contact` `Team_team_id_Contact` ON ((
					`WorkOrder`.`team_id` = `Team_team_id_Contact`.`id` 
				)))
		LEFT JOIN (
			`person` `Person_agent_id`
			JOIN `contact` `Person_agent_id_Contact` ON ((
					`Person_agent_id`.`id` = `Person_agent_id_Contact`.`id` 
					))) ON ((
				`WorkOrder`.`owner_id` = `Person_agent_id`.`id` 
			))) 
WHERE
	(
	0 <> COALESCE (( `Team_team_id_Contact`.`finalclass` = 'Team' ), 1 ))
```

