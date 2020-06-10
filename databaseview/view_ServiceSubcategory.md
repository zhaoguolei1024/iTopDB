| 列                               | 类型                                                     | 注释 |
| :------------------------------- | -------------------------------------------------------- | ---- |
| id                               | int [**0**]                                              |      |
| name                             | varchar(255) *NULL* []                                   |      |
| description                      | text *NULL*                                              |      |
| service_id                       | int *NULL* [**0**]                                       |      |
| service_org_id                   | int *NULL* [**0**]                                       |      |
| service_name                     | varchar(255) *NULL* []                                   |      |
| service_provider                 | varchar(255) *NULL* []                                   |      |
| request_type                     | enum('incident','service_request') *NULL* [**incident**] |      |
| status                           | enum('implementation','obsolete','production') *NULL*    |      |
| friendlyname                     | varchar(255) *NULL*                                      |      |
| service_id_friendlyname          | varchar(255) *NULL*                                      |      |
| service_org_id_friendlyname      | varchar(255) *NULL*                                      |      |
| service_org_id_obsolescence_flag | int [**0**]                                              |      |

```
SELECT DISTINCT
	`ServiceSubcategory`.`id` AS `id`,
	`ServiceSubcategory`.`name` AS `name`,
	`ServiceSubcategory`.`description` AS `description`,
	`ServiceSubcategory`.`service_id` AS `service_id`,
	`Service_service_id`.`org_id` AS `service_org_id`,
	`Service_service_id`.`name` AS `service_name`,
	`Organization_org_id`.`name` AS `service_provider`,
	`ServiceSubcategory`.`request_type` AS `request_type`,
	`ServiceSubcategory`.`status` AS `status`,
	cast( concat( COALESCE ( `ServiceSubcategory`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `friendlyname`,
	cast( concat( COALESCE ( `Service_service_id`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `service_id_friendlyname`,
	cast( concat( COALESCE ( `Organization_org_id`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `service_org_id_friendlyname`,
	COALESCE (( `Organization_org_id`.`status` = 'inactive' ), 0 ) AS `service_org_id_obsolescence_flag` 
FROM
	(
		`servicesubcategory` `ServiceSubcategory`
		JOIN (
			`service` `Service_service_id`
			JOIN `organization` `Organization_org_id` ON ((
					`Service_service_id`.`org_id` = `Organization_org_id`.`id` 
					))) ON ((
				`ServiceSubcategory`.`service_id` = `Service_service_id`.`id` 
			))) 
WHERE
	(
	0 <> 1)
```

