| 列                       | 类型                                                         | 注释 |
| :----------------------- | ------------------------------------------------------------ | ---- |
| id                       | int [**0**]                                                  |      |
| name                     | varchar(255) *NULL* []                                       |      |
| org_id                   | int *NULL* [**0**]                                           |      |
| cust_name                | varchar(255) *NULL* []                                       |      |
| problem_id               | int *NULL* [**0**]                                           |      |
| problem_ref              | varchar(255) *NULL* []                                       |      |
| symptom                  | text *NULL*                                                  |      |
| root_cause               | text *NULL*                                                  |      |
| workaround               | text *NULL*                                                  |      |
| solution                 | text *NULL*                                                  |      |
| error_code               | varchar(255) *NULL* []                                       |      |
| domain                   | enum('Application','Desktop','Network','Server') *NULL* [**Application**] |      |
| vendor                   | varchar(255) *NULL* []                                       |      |
| model                    | varchar(255) *NULL* []                                       |      |
| version                  | varchar(255) *NULL* []                                       |      |
| friendlyname             | varchar(255) *NULL*                                          |      |
| org_id_friendlyname      | varchar(255) *NULL*                                          |      |
| org_id_obsolescence_flag | int [**0**]                                                  |      |
| problem_id_friendlyname  | varchar(255) *NULL*                                          |      |

```
select distinct `KnownError`.`id` AS `id`,`KnownError`.`name` AS `name`,`KnownError`.`cust_id` AS `org_id`,`Organization_org_id`.`name` AS `cust_name`,`KnownError`.`problem_id` AS `problem_id`,`Problem_problem_id_Ticket`.`ref` AS `problem_ref`,`KnownError`.`symptom` AS `symptom`,`KnownError`.`rootcause` AS `root_cause`,`KnownError`.`workaround` AS `workaround`,`KnownError`.`solution` AS `solution`,`KnownError`.`error_code` AS `error_code`,`KnownError`.`domain` AS `domain`,`KnownError`.`vendor` AS `vendor`,`KnownError`.`model` AS `model`,`KnownError`.`version` AS `version`,cast(concat(coalesce(`KnownError`.`name`,'')) as char charset utf8mb4) AS `friendlyname`,cast(concat(coalesce(`Organization_org_id`.`name`,'')) as char charset utf8mb4) AS `org_id_friendlyname`,coalesce((`Organization_org_id`.`status` = 'inactive'),0) AS `org_id_obsolescence_flag`,cast(concat(coalesce(`Problem_problem_id_Ticket`.`ref`,'')) as char charset utf8mb4) AS `problem_id_friendlyname` from ((`knownerror` `KnownError` join `organization` `Organization_org_id` on((`KnownError`.`cust_id` = `Organization_org_id`.`id`))) left join `ticket` `Problem_problem_id_Ticket` on((`KnownError`.`problem_id` = `Problem_problem_id_Ticket`.`id`))) where (0 <> coalesce((`Problem_problem_id_Ticket`.`finalclass` = 'Problem'),1))
```

