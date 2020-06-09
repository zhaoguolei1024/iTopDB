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
| finalclass               | varchar(255) *NULL* [**FunctionalCI**]                       |      |
| friendlyname             | varchar(255) *NULL*                                          |      |
| obsolescence_flag        | int [**0**]                                                  |      |
| obsolescence_date        | date *NULL*                                                  |      |
| org_id_friendlyname      | varchar(255) *NULL*                                          |      |
| org_id_obsolescence_flag | int [**0**]                                                  |      |

```
select distinct `VirtualHost_VirtualDevice`.`id` AS `id`,`VirtualHost_FunctionalCI`.`name` AS `name`,`VirtualHost_FunctionalCI`.`description` AS `description`,`VirtualHost_FunctionalCI`.`org_id` AS `org_id`,`Organization_org_id`.`name` AS `organization_name`,`VirtualHost_FunctionalCI`.`business_criticity` AS `business_criticity`,`VirtualHost_FunctionalCI`.`move2production` AS `move2production`,`VirtualHost_VirtualDevice`.`status` AS `status`,`VirtualHost_FunctionalCI`.`finalclass` AS `finalclass`,cast(concat(coalesce(`VirtualHost_FunctionalCI`.`name`,'')) as char charset utf8mb4) AS `friendlyname`,coalesce((`VirtualHost_VirtualDevice`.`status` = 'obsolete'),0) AS `obsolescence_flag`,`VirtualHost_FunctionalCI`.`obsolescence_date` AS `obsolescence_date`,cast(concat(coalesce(`Organization_org_id`.`name`,'')) as char charset utf8mb4) AS `org_id_friendlyname`,coalesce((`Organization_org_id`.`status` = 'inactive'),0) AS `org_id_obsolescence_flag` from (`virtualdevice` `VirtualHost_VirtualDevice` join (`functionalci` `VirtualHost_FunctionalCI` join `organization` `Organization_org_id` on((`VirtualHost_FunctionalCI`.`org_id` = `Organization_org_id`.`id`))) on((`VirtualHost_VirtualDevice`.`id` = `VirtualHost_FunctionalCI`.`id`))) where (0 <> coalesce((`VirtualHost_VirtualDevice`.`finalclass` in ('Hypervisor','Farm','VirtualHost')),1))
```

