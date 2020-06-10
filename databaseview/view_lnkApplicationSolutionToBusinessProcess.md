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
SELECT DISTINCT
	`lnkApplicationSolutionToBusinessProcess`.`id` AS `id`,
	`lnkApplicationSolutionToBusinessProcess`.`businessprocess_id` AS `businessprocess_id`,
	`BusinessProcess_businessprocess_id_FunctionalCI`.`name` AS `businessprocess_name`,
	`lnkApplicationSolutionToBusinessProcess`.`applicationsolution_id` AS `applicationsolution_id`,
	`ApplicationSolution_applicationsolution_id_FunctionalCI`.`name` AS `applicationsolution_name`,
	cast(
		concat(
			COALESCE ( `lnkApplicationSolutionToBusinessProcess`.`businessprocess_id`, '' ),
			COALESCE ( ' ', '' ),
		COALESCE ( `lnkApplicationSolutionToBusinessProcess`.`applicationsolution_id`, '' )) AS CHAR charset utf8mb4 
	) AS `friendlyname`,
	cast( concat( COALESCE ( `BusinessProcess_businessprocess_id_FunctionalCI`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `businessprocess_id_friendlyname`,
	COALESCE (( `BusinessProcess_businessprocess_id`.`status` = 'inactive' ), 0 ) AS `businessprocess_id_obsolescence_flag`,
	cast( concat( COALESCE ( `ApplicationSolution_applicationsolution_id_FunctionalCI`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `applicationsolution_id_friendlyname`,
	COALESCE (( `ApplicationSolution_applicationsolution_id`.`status` = 'inactive' ), 0 ) AS `applicationsolution_id_obsolescence_flag` 
FROM
	((
			`lnkapplicationsolutiontobusinessprocess` `lnkApplicationSolutionToBusinessProcess`
			JOIN (
				`businessprocess` `BusinessProcess_businessprocess_id`
				JOIN `functionalci` `BusinessProcess_businessprocess_id_FunctionalCI` ON ((
						`BusinessProcess_businessprocess_id`.`id` = `BusinessProcess_businessprocess_id_FunctionalCI`.`id` 
						))) ON ((
					`lnkApplicationSolutionToBusinessProcess`.`businessprocess_id` = `BusinessProcess_businessprocess_id`.`id` 
				)))
		JOIN (
			`applicationsolution` `ApplicationSolution_applicationsolution_id`
			JOIN `functionalci` `ApplicationSolution_applicationsolution_id_FunctionalCI` ON ((
					`ApplicationSolution_applicationsolution_id`.`id` = `ApplicationSolution_applicationsolution_id_FunctionalCI`.`id` 
					))) ON ((
				`lnkApplicationSolutionToBusinessProcess`.`applicationsolution_id` = `ApplicationSolution_applicationsolution_id`.`id` 
			))) 
WHERE
	(
	0 <> 1)
```

