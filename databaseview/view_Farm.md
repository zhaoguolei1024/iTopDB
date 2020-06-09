| 列                       | 类型                                                         | 注释 |
| :----------------------- | ------------------------------------------------------------ | ---- |
| id                       | int [**0**]                                                  |      |
| name                     | varchar(255) *NULL* []                                       |      |
| description              | text *NULL*                                                  |      |
| org_id                   | int *NULL* [**0**]                                           |      |
| organization_name        | varchar(255) *NULL* []                                       |      |
| business_criticity       | enum('high','low','medium') *NULL* [**low**]                 |      |
| move2production          | date *NULL*                                                  |      |
| status                   | enum('implementation','obsolete','production','stock') *NULL* [**production**] |      |
| redundancy               | varchar(20) *NULL* [**1**]                                   |      |
| finalclass               | varchar(255) *NULL* [**FunctionalCI**]                       |      |
| friendlyname             | varchar(255) *NULL*                                          |      |
| obsolescence_flag        | int [**0**]                                                  |      |
| obsolescence_date        | date *NULL*                                                  |      |
| org_id_friendlyname      | varchar(255) *NULL*                                          |      |
| org_id_obsolescence_flag | int [**0**]                                                  |      |

```
select distinct `Farm`.`id` AS `id`,`Farm_FunctionalCI`.`name` AS `name`,`Farm_FunctionalCI`.`description` AS `description`,`Farm_FunctionalCI`.`org_id` AS `org_id`,`Organization_org_id`.`name` AS `organization_name`,`Farm_FunctionalCI`.`business_criticity` AS `business_criticity`,`Farm_FunctionalCI`.`move2production` AS `move2production`,`Farm_VirtualDevice`.`status` AS `status`,`Farm`.`redundancy` AS `redundancy`,`Farm_FunctionalCI`.`finalclass` AS `finalclass`,cast(concat(coalesce(`Farm_FunctionalCI`.`name`,'')) as char charset utf8mb4) AS `friendlyname`,coalesce((`Farm_VirtualDevice`.`status` = 'obsolete'),0) AS `obsolescence_flag`,`Farm_FunctionalCI`.`obsolescence_date` AS `obsolescence_date`,cast(concat(coalesce(`Organization_org_id`.`name`,'')) as char charset utf8mb4) AS `org_id_friendlyname`,coalesce((`Organization_org_id`.`status` = 'inactive'),0) AS `org_id_obsolescence_flag` from ((`farm` `Farm` join `virtualdevice` `Farm_VirtualDevice` on((`Farm`.`id` = `Farm_VirtualDevice`.`id`))) join (`functionalci` `Farm_FunctionalCI` join `organization` `Organization_org_id` on((`Farm_FunctionalCI`.`org_id` = `Organization_org_id`.`id`))) on((`Farm`.`id` = `Farm_FunctionalCI`.`id`))) where (0 <> 1)
```

