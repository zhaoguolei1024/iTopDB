| 列                          | 类型                                                         | 注释 |
| :-------------------------- | ------------------------------------------------------------ | ---- |
| id                          | int [**0**]                                                  |      |
| name                        | varchar(255) *NULL* []                                       |      |
| status                      | enum('implementation','obsolete','production') *NULL* [**implementation**] |      |
| org_id                      | int *NULL* [**0**]                                           |      |
| owner_name                  | varchar(255) *NULL* []                                       |      |
| description                 | text *NULL*                                                  |      |
| type                        | varchar(255) *NULL* []                                       |      |
| parent_id                   | int *NULL* [**0**]                                           |      |
| parent_name                 | varchar(255) *NULL* []                                       |      |
| friendlyname                | varchar(255) *NULL*                                          |      |
| obsolescence_flag           | int [**0**]                                                  |      |
| obsolescence_date           | date *NULL*                                                  |      |
| org_id_friendlyname         | varchar(255) *NULL*                                          |      |
| org_id_obsolescence_flag    | int [**0**]                                                  |      |
| parent_id_friendlyname      | varchar(255) *NULL*                                          |      |
| parent_id_obsolescence_flag | int [**0**]                                                  |      |

```
select distinct `Group`.`id` AS `id`,`Group`.`name` AS `name`,`Group`.`status` AS `status`,`Group`.`org_id` AS `org_id`,`Organization_org_id`.`name` AS `owner_name`,`Group`.`description` AS `description`,`Group`.`type` AS `type`,`Group`.`parent_id` AS `parent_id`,`Group_parent_id`.`name` AS `parent_name`,cast(concat(coalesce(`Group`.`name`,'')) as char charset utf8mb4) AS `friendlyname`,coalesce((`Group`.`status` = 'obsolete'),0) AS `obsolescence_flag`,`Group`.`obsolescence_date` AS `obsolescence_date`,cast(concat(coalesce(`Organization_org_id`.`name`,'')) as char charset utf8mb4) AS `org_id_friendlyname`,coalesce((`Organization_org_id`.`status` = 'inactive'),0) AS `org_id_obsolescence_flag`,cast(concat(coalesce(`Group_parent_id`.`name`,'')) as char charset utf8mb4) AS `parent_id_friendlyname`,coalesce((`Group_parent_id`.`status` = 'obsolete'),0) AS `parent_id_obsolescence_flag` from ((`group` `Group` join `organization` `Organization_org_id` on((`Group`.`org_id` = `Organization_org_id`.`id`))) left join `group` `Group_parent_id` on((`Group`.`parent_id` = `Group_parent_id`.`id`))) where (0 <> 1)
```

