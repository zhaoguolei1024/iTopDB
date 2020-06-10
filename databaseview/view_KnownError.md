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
SELECT DISTINCT
	`KnownError`.`id` AS `id`,
	`KnownError`.`name` AS `name`,
	`KnownError`.`cust_id` AS `org_id`,
	`Organization_org_id`.`name` AS `cust_name`,
	`KnownError`.`problem_id` AS `problem_id`,
	`Problem_problem_id_Ticket`.`ref` AS `problem_ref`,
	`KnownError`.`symptom` AS `symptom`,
	`KnownError`.`rootcause` AS `root_cause`,
	`KnownError`.`workaround` AS `workaround`,
	`KnownError`.`solution` AS `solution`,
	`KnownError`.`error_code` AS `error_code`,
	`KnownError`.`domain` AS `domain`,
	`KnownError`.`vendor` AS `vendor`,
	`KnownError`.`model` AS `model`,
	`KnownError`.`version` AS `version`,
	cast( concat( COALESCE ( `KnownError`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `friendlyname`,
	cast( concat( COALESCE ( `Organization_org_id`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `org_id_friendlyname`,
	COALESCE (( `Organization_org_id`.`status` = 'inactive' ), 0 ) AS `org_id_obsolescence_flag`,
	cast( concat( COALESCE ( `Problem_problem_id_Ticket`.`ref`, '' )) AS CHAR charset utf8mb4 ) AS `problem_id_friendlyname` 
FROM
	((
			`knownerror` `KnownError`
			JOIN `organization` `Organization_org_id` ON ((
					`KnownError`.`cust_id` = `Organization_org_id`.`id` 
				)))
		LEFT JOIN `ticket` `Problem_problem_id_Ticket` ON ((
				`KnownError`.`problem_id` = `Problem_problem_id_Ticket`.`id` 
			))) 
WHERE
	(
	0 <> COALESCE (( `Problem_problem_id_Ticket`.`finalclass` = 'Problem' ), 1 ))
```

