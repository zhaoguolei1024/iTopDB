| 列                           | 类型                                        | 注释 |
| :--------------------------- | ------------------------------------------- | ---- |
| id                           | int [**0**]                                 |      |
| name                         | varchar(255) *NULL* []                      |      |
| org_id                       | int *NULL* [**0**]                          |      |
| org_name                     | varchar(255) *NULL* []                      |      |
| documenttype_id              | int *NULL* [**0**]                          |      |
| documenttype_name            | varchar(255) *NULL* []                      |      |
| version                      | varchar(255) *NULL* []                      |      |
| description                  | text *NULL*                                 |      |
| status                       | enum('draft','obsolete','published') *NULL* |      |
| url                          | varchar(2048) *NULL* []                     |      |
| finalclass                   | varchar(255) *NULL* [**Document**]          |      |
| friendlyname                 | varchar(255) *NULL*                         |      |
| obsolescence_flag            | int [**0**]                                 |      |
| obsolescence_date            | date *NULL*                                 |      |
| org_id_friendlyname          | varchar(255) *NULL*                         |      |
| org_id_obsolescence_flag     | int [**0**]                                 |      |
| documenttype_id_friendlyname | varchar(255) *NULL*                         |      |

```
SELECT DISTINCT
	`DocumentWeb`.`id` AS `id`,
	`DocumentWeb_Document`.`name` AS `name`,
	`DocumentWeb_Document`.`org_id` AS `org_id`,
	`Organization_org_id`.`name` AS `org_name`,
	`DocumentWeb_Document`.`documenttype_id` AS `documenttype_id`,
	`DocumentType_documenttype_id_Typology`.`name` AS `documenttype_name`,
	`DocumentWeb_Document`.`version` AS `version`,
	`DocumentWeb_Document`.`description` AS `description`,
	`DocumentWeb_Document`.`status` AS `status`,
	`DocumentWeb`.`url` AS `url`,
	`DocumentWeb_Document`.`finalclass` AS `finalclass`,
	cast( concat( COALESCE ( `DocumentWeb_Document`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `friendlyname`,
	COALESCE (( `DocumentWeb_Document`.`status` = 'obsolete' ), 0 ) AS `obsolescence_flag`,
	`DocumentWeb_Document`.`obsolescence_date` AS `obsolescence_date`,
	cast( concat( COALESCE ( `Organization_org_id`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `org_id_friendlyname`,
	COALESCE (( `Organization_org_id`.`status` = 'inactive' ), 0 ) AS `org_id_obsolescence_flag`,
	cast( concat( COALESCE ( `DocumentType_documenttype_id_Typology`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `documenttype_id_friendlyname` 
FROM
	(
		`documentweb` `DocumentWeb`
		JOIN ((
				`document` `DocumentWeb_Document`
				JOIN `organization` `Organization_org_id` ON ((
						`DocumentWeb_Document`.`org_id` = `Organization_org_id`.`id` 
					)))
			LEFT JOIN `typology` `DocumentType_documenttype_id_Typology` ON ((
					`DocumentWeb_Document`.`documenttype_id` = `DocumentType_documenttype_id_Typology`.`id` 
					))) ON ((
				`DocumentWeb`.`id` = `DocumentWeb_Document`.`id` 
			))) 
WHERE
	(
	0 <> COALESCE (( `DocumentType_documenttype_id_Typology`.`finalclass` = 'DocumentType' ), 1 ))
```

