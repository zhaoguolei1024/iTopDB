|                          |                                               |                                        |
| :----------------------- | --------------------------------------------- | -------------------------------------- |
| 列                       | 类型                                          | 注释                                   |
| id                       | int [**0**]                                   | 关联FunctionalCI数据表的ID             |
| name                     | varchar(255) *NULL* []                        |                                        |
| description              | text *NULL*                                   |                                        |
| org_id                   | int *NULL* [**0**]                            |                                        |
| organization_name        | varchar(255) *NULL* []                        |                                        |
| business_criticity       | enum('high','low','medium') *NULL* [**low**]  |                                        |
| move2production          | date *NULL*                                   |                                        |
| status                   | enum('active','inactive') *NULL* [**active**] | 是否启用，启用为active，禁用为inactive |
| redundancy               | varchar(20) *NULL* [**disabled**]             | 冗余配置                               |
| finalclass               | varchar(255) *NULL* [**FunctionalCI**]        |                                        |
| friendlyname             | varchar(255) []                               |                                        |
| obsolescence_flag        | int [**0**]                                   |                                        |
| obsolescence_date        | date *NULL*                                   |                                        |
| org_id_friendlyname      | varchar(255) []                               |                                        |
| org_id_obsolescence_flag | int [**0**]                                   |                                        |

```
SELECT DISTINCT
	`ApplicationSolution`.`id` AS `id`,
	`ApplicationSolution_FunctionalCI`.`name` AS `name`,
	`ApplicationSolution_FunctionalCI`.`description` AS `description`,
	`ApplicationSolution_FunctionalCI`.`org_id` AS `org_id`,
	`Organization_org_id`.`name` AS `organization_name`,
	`ApplicationSolution_FunctionalCI`.`business_criticity` AS `business_criticity`,
	`ApplicationSolution_FunctionalCI`.`move2production` AS `move2production`,
	`ApplicationSolution`.`status` AS `status`,
	`ApplicationSolution`.`redundancy` AS `redundancy`,
	`ApplicationSolution_FunctionalCI`.`finalclass` AS `finalclass`,
	cast( concat( COALESCE ( `ApplicationSolution_FunctionalCI`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `friendlyname`,
	COALESCE (( `ApplicationSolution`.`status` = 'inactive' ), 0 ) AS `obsolescence_flag`,
	`ApplicationSolution_FunctionalCI`.`obsolescence_date` AS `obsolescence_date`,
	cast( concat( COALESCE ( `Organization_org_id`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `org_id_friendlyname`,
	COALESCE (( `Organization_org_id`.`status` = 'inactive' ), 0 ) AS `org_id_obsolescence_flag` 
FROM
	(
		`applicationsolution` `ApplicationSolution`
		JOIN (
			`functionalci` `ApplicationSolution_FunctionalCI`
			JOIN `organization` `Organization_org_id` ON ((
					`ApplicationSolution_FunctionalCI`.`org_id` = `Organization_org_id`.`id` 
					))) ON ((
				`ApplicationSolution`.`id` = `ApplicationSolution_FunctionalCI`.`id` 
			))) 
WHERE
	(
	0 <> 1)
```

