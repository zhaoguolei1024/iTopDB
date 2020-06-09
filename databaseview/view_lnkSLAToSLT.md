| 列                  | 类型                                      | 注释 |
| :------------------ | ----------------------------------------- | ---- |
| id                  | int [**0**]                               |      |
| sla_id              | int *NULL* [**0**]                        |      |
| sla_name            | varchar(255) *NULL* []                    |      |
| slt_id              | int *NULL* [**0**]                        |      |
| slt_name            | varchar(255) *NULL* []                    |      |
| slt_metric          | enum('tto','ttr') *NULL*                  |      |
| slt_request_type    | enum('incident','service_request') *NULL* |      |
| slt_ticket_priority | enum('1','2','3','4') *NULL*              |      |
| slt_value           | int *NULL*                                |      |
| slt_value_unit      | enum('hours','minutes') *NULL*            |      |
| friendlyname        | varchar(23) *NULL*                        |      |
| sla_id_friendlyname | varchar(255) *NULL*                       |      |
| slt_id_friendlyname | varchar(255) *NULL*                       |      |

```
select distinct `lnkSLAToSLT`.`id` AS `id`,`lnkSLAToSLT`.`sla_id` AS `sla_id`,`SLA_sla_id`.`name` AS `sla_name`,`lnkSLAToSLT`.`slt_id` AS `slt_id`,`SLT_slt_id`.`name` AS `slt_name`,`SLT_slt_id`.`metric` AS `slt_metric`,`SLT_slt_id`.`request_type` AS `slt_request_type`,`SLT_slt_id`.`priority` AS `slt_ticket_priority`,`SLT_slt_id`.`value` AS `slt_value`,`SLT_slt_id`.`unit` AS `slt_value_unit`,cast(concat(coalesce(`lnkSLAToSLT`.`sla_id`,''),coalesce(' ',''),coalesce(`lnkSLAToSLT`.`slt_id`,'')) as char charset utf8mb4) AS `friendlyname`,cast(concat(coalesce(`SLA_sla_id`.`name`,'')) as char charset utf8mb4) AS `sla_id_friendlyname`,cast(concat(coalesce(`SLT_slt_id`.`name`,'')) as char charset utf8mb4) AS `slt_id_friendlyname` from ((`lnkslatoslt` `lnkSLAToSLT` join `sla` `SLA_sla_id` on((`lnkSLAToSLT`.`sla_id` = `SLA_sla_id`.`id`))) join `slt` `SLT_slt_id` on((`lnkSLAToSLT`.`slt_id` = `SLT_slt_id`.`id`))) where (0 <> 1)
```

