| 列                                       | 类型                   | 注释 |
| :--------------------------------------- | ---------------------- | ---- |
| id                                       | int [**0**]            |      |
| businessprocess_id                       | int *NULL* [**0**]     |      |
| businessprocess_name                     | varchar(255) *NULL* [] |      |
| applicationsolution_id                   | int *NULL* [**0**]     |      |
| applicationsolution_name                 | varchar(255) *NULL* [] |      |
| friendlyname                             | varchar(23) []         |      |
| businessprocess_id_friendlyname          | varchar(255) []        |      |
| businessprocess_id_obsolescence_flag     | int [**0**]            |      |
| applicationsolution_id_friendlyname      | varchar(255) []        |      |
| applicationsolution_id_obsolescence_flag | int [**0**]            |      |

```
select distinct `lnkApplicationSolutionToBusinessProcess`.`id` AS `id`,`lnkApplicationSolutionToBusinessProcess`.`businessprocess_id` AS `businessprocess_id`,`BusinessProcess_businessprocess_id_FunctionalCI`.`name` AS `businessprocess_name`,`lnkApplicationSolutionToBusinessProcess`.`applicationsolution_id` AS `applicationsolution_id`,`ApplicationSolution_applicationsolution_id_FunctionalCI`.`name` AS `applicationsolution_name`,cast(concat(coalesce(`lnkApplicationSolutionToBusinessProcess`.`businessprocess_id`,''),coalesce(' ',''),coalesce(`lnkApplicationSolutionToBusinessProcess`.`applicationsolution_id`,'')) as char charset utf8mb4) AS `friendlyname`,cast(concat(coalesce(`BusinessProcess_businessprocess_id_FunctionalCI`.`name`,'')) as char charset utf8mb4) AS `businessprocess_id_friendlyname`,coalesce((`BusinessProcess_businessprocess_id`.`status` = 'inactive'),0) AS `businessprocess_id_obsolescence_flag`,cast(concat(coalesce(`ApplicationSolution_applicationsolution_id_FunctionalCI`.`name`,'')) as char charset utf8mb4) AS `applicationsolution_id_friendlyname`,coalesce((`ApplicationSolution_applicationsolution_id`.`status` = 'inactive'),0) AS `applicationsolution_id_obsolescence_flag` from ((`lnkapplicationsolutiontobusinessprocess` `lnkApplicationSolutionToBusinessProcess` join (`businessprocess` `BusinessProcess_businessprocess_id` join `functionalci` `BusinessProcess_businessprocess_id_FunctionalCI` on((`BusinessProcess_businessprocess_id`.`id` = `BusinessProcess_businessprocess_id_FunctionalCI`.`id`))) on((`lnkApplicationSolutionToBusinessProcess`.`businessprocess_id` = `BusinessProcess_businessprocess_id`.`id`))) join (`applicationsolution` `ApplicationSolution_applicationsolution_id` join `functionalci` `ApplicationSolution_applicationsolution_id_FunctionalCI` on((`ApplicationSolution_applicationsolution_id`.`id` = `ApplicationSolution_applicationsolution_id_FunctionalCI`.`id`))) on((`lnkApplicationSolutionToBusinessProcess`.`applicationsolution_id` = `ApplicationSolution_applicationsolution_id`.`id`))) where (0 <> 1)
```

