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
SELECT DISTINCT
	`lnkSLAToSLT`.`id` AS `id`,
	`lnkSLAToSLT`.`sla_id` AS `sla_id`,
	`SLA_sla_id`.`name` AS `sla_name`,
	`lnkSLAToSLT`.`slt_id` AS `slt_id`,
	`SLT_slt_id`.`name` AS `slt_name`,
	`SLT_slt_id`.`metric` AS `slt_metric`,
	`SLT_slt_id`.`request_type` AS `slt_request_type`,
	`SLT_slt_id`.`priority` AS `slt_ticket_priority`,
	`SLT_slt_id`.`value` AS `slt_value`,
	`SLT_slt_id`.`unit` AS `slt_value_unit`,
	cast(
		concat(
			COALESCE ( `lnkSLAToSLT`.`sla_id`, '' ),
			COALESCE ( ' ', '' ),
		COALESCE ( `lnkSLAToSLT`.`slt_id`, '' )) AS CHAR charset utf8mb4 
	) AS `friendlyname`,
	cast( concat( COALESCE ( `SLA_sla_id`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `sla_id_friendlyname`,
	cast( concat( COALESCE ( `SLT_slt_id`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `slt_id_friendlyname` 
FROM
	((
			`lnkslatoslt` `lnkSLAToSLT`
			JOIN `sla` `SLA_sla_id` ON ((
					`lnkSLAToSLT`.`sla_id` = `SLA_sla_id`.`id` 
				)))
		JOIN `slt` `SLT_slt_id` ON ((
				`lnkSLAToSLT`.`slt_id` = `SLT_slt_id`.`id` 
			))) 
WHERE
	(
	0 <> 1)
```

