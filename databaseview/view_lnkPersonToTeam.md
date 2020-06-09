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
select distinct `lnkPersonToTeam`.`id` AS `id`,`lnkPersonToTeam`.`team_id` AS `team_id`,`Team_team_id_Contact`.`name` AS `team_name`,`lnkPersonToTeam`.`person_id` AS `person_id`,`Person_person_id_Contact`.`name` AS `person_name`,`lnkPersonToTeam`.`role_id` AS `role_id`,`ContactType_role_id_Typology`.`name` AS `role_name`,cast(concat(coalesce(`lnkPersonToTeam`.`team_id`,''),coalesce(' ',''),coalesce(`lnkPersonToTeam`.`person_id`,'')) as char charset utf8mb4) AS `friendlyname`,cast(concat(coalesce(`Team_team_id_Contact`.`name`,'')) as char charset utf8mb4) AS `team_id_friendlyname`,coalesce((`Team_team_id_Contact`.`status` = 'inactive'),0) AS `team_id_obsolescence_flag`,cast(concat(coalesce(`Person_person_id`.`first_name`,''),coalesce(' ',''),coalesce(`Person_person_id_Contact`.`name`,'')) as char charset utf8mb4) AS `person_id_friendlyname`,coalesce((`Person_person_id_Contact`.`status` = 'inactive'),0) AS `person_id_obsolescence_flag`,cast(concat(coalesce(`ContactType_role_id_Typology`.`name`,'')) as char charset utf8mb4) AS `role_id_friendlyname` from (((`lnkpersontoteam` `lnkPersonToTeam` join `contact` `Team_team_id_Contact` on((`lnkPersonToTeam`.`team_id` = `Team_team_id_Contact`.`id`))) join (`person` `Person_person_id` join `contact` `Person_person_id_Contact` on((`Person_person_id`.`id` = `Person_person_id_Contact`.`id`))) on((`lnkPersonToTeam`.`person_id` = `Person_person_id`.`id`))) left join `typology` `ContactType_role_id_Typology` on((`lnkPersonToTeam`.`role_id` = `ContactType_role_id_Typology`.`id`))) where ((0 <> coalesce((`Team_team_id_Contact`.`finalclass` = 'Team'),1)) and (0 <> coalesce((`ContactType_role_id_Typology`.`finalclass` = 'ContactType'),1)))
```

