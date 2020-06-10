| 列                          | 类型                   | 注释 |
| :-------------------------- | ---------------------- | ---- |
| id                          | int [**0**]            |      |
| team_id                     | int *NULL* [**0**]     |      |
| team_name                   | varchar(255) *NULL* [] |      |
| person_id                   | int *NULL* [**0**]     |      |
| person_name                 | varchar(255) *NULL* [] |      |
| role_id                     | int *NULL* [**0**]     |      |
| role_name                   | varchar(255) *NULL* [] |      |
| friendlyname                | varchar(23) *NULL*     |      |
| team_id_friendlyname        | varchar(255) *NULL*    |      |
| team_id_obsolescence_flag   | int [**0**]            |      |
| person_id_friendlyname      | varchar(511) *NULL*    |      |
| person_id_obsolescence_flag | int [**0**]            |      |
| role_id_friendlyname        | varchar(255) *NULL*    |      |

```
SELECT DISTINCT
	`lnkPersonToTeam`.`id` AS `id`,
	`lnkPersonToTeam`.`team_id` AS `team_id`,
	`Team_team_id_Contact`.`name` AS `team_name`,
	`lnkPersonToTeam`.`person_id` AS `person_id`,
	`Person_person_id_Contact`.`name` AS `person_name`,
	`lnkPersonToTeam`.`role_id` AS `role_id`,
	`ContactType_role_id_Typology`.`name` AS `role_name`,
	cast(
		concat(
			COALESCE ( `lnkPersonToTeam`.`team_id`, '' ),
			COALESCE ( ' ', '' ),
		COALESCE ( `lnkPersonToTeam`.`person_id`, '' )) AS CHAR charset utf8mb4 
	) AS `friendlyname`,
	cast( concat( COALESCE ( `Team_team_id_Contact`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `team_id_friendlyname`,
	COALESCE (( `Team_team_id_Contact`.`status` = 'inactive' ), 0 ) AS `team_id_obsolescence_flag`,
	cast(
		concat(
			COALESCE ( `Person_person_id`.`first_name`, '' ),
			COALESCE ( ' ', '' ),
		COALESCE ( `Person_person_id_Contact`.`name`, '' )) AS CHAR charset utf8mb4 
	) AS `person_id_friendlyname`,
	COALESCE (( `Person_person_id_Contact`.`status` = 'inactive' ), 0 ) AS `person_id_obsolescence_flag`,
	cast( concat( COALESCE ( `ContactType_role_id_Typology`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `role_id_friendlyname` 
FROM
	(((
				`lnkpersontoteam` `lnkPersonToTeam`
				JOIN `contact` `Team_team_id_Contact` ON ((
						`lnkPersonToTeam`.`team_id` = `Team_team_id_Contact`.`id` 
					)))
			JOIN (
				`person` `Person_person_id`
				JOIN `contact` `Person_person_id_Contact` ON ((
						`Person_person_id`.`id` = `Person_person_id_Contact`.`id` 
						))) ON ((
					`lnkPersonToTeam`.`person_id` = `Person_person_id`.`id` 
				)))
		LEFT JOIN `typology` `ContactType_role_id_Typology` ON ((
				`lnkPersonToTeam`.`role_id` = `ContactType_role_id_Typology`.`id` 
			))) 
WHERE
	((
			0 <> COALESCE (( `Team_team_id_Contact`.`finalclass` = 'Team' ), 1 )) 
	AND (
	0 <> COALESCE (( `ContactType_role_id_Typology`.`finalclass` = 'ContactType' ), 1 )))
```

