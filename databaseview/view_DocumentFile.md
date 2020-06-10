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
| file                         | varchar(255) *NULL*                         |      |
| finalclass                   | varchar(255) *NULL* [**Document**]          |      |
| friendlyname                 | varchar(255) *NULL*                         |      |
| obsolescence_flag            | int [**0**]                                 |      |
| obsolescence_date            | date *NULL*                                 |      |
| org_id_friendlyname          | varchar(255) *NULL*                         |      |
| org_id_obsolescence_flag     | int [**0**]                                 |      |
| documenttype_id_friendlyname | varchar(255) *NULL*                         |      |
| DocumentFilefile_data        | longblob *NULL*                             |      |
| DocumentFilefile_filename    | varchar(255) *NULL*                         |      |

```
SELECT DISTINCT
	`DocumentFile`.`id` AS `id`,
	`DocumentFile_Document`.`name` AS `name`,
	`DocumentFile_Document`.`org_id` AS `org_id`,
	`Organization_org_id`.`name` AS `org_name`,
	`DocumentFile_Document`.`documenttype_id` AS `documenttype_id`,
	`DocumentType_documenttype_id_Typology`.`name` AS `documenttype_name`,
	`DocumentFile_Document`.`version` AS `version`,
	`DocumentFile_Document`.`description` AS `description`,
	`DocumentFile_Document`.`status` AS `status`,
	`DocumentFile`.`file_mimetype` AS `file`,
	`DocumentFile_Document`.`finalclass` AS `finalclass`,
	cast( concat( COALESCE ( `DocumentFile_Document`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `friendlyname`,
	COALESCE (( `DocumentFile_Document`.`status` = 'obsolete' ), 0 ) AS `obsolescence_flag`,
	`DocumentFile_Document`.`obsolescence_date` AS `obsolescence_date`,
	cast( concat( COALESCE ( `Organization_org_id`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `org_id_friendlyname`,
	COALESCE (( `Organization_org_id`.`status` = 'inactive' ), 0 ) AS `org_id_obsolescence_flag`,
	cast( concat( COALESCE ( `DocumentType_documenttype_id_Typology`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `documenttype_id_friendlyname`,
	`DocumentFile`.`file_data` AS `DocumentFilefile_data`,
	`DocumentFile`.`file_filename` AS `DocumentFilefile_filename` 
FROM
	(
		`documentfile` `DocumentFile`
		JOIN ((
				`document` `DocumentFile_Document`
				JOIN `organization` `Organization_org_id` ON ((
						`DocumentFile_Document`.`org_id` = `Organization_org_id`.`id` 
					)))
			LEFT JOIN `typology` `DocumentType_documenttype_id_Typology` ON ((
					`DocumentFile_Document`.`documenttype_id` = `DocumentType_documenttype_id_Typology`.`id` 
					))) ON ((
				`DocumentFile`.`id` = `DocumentFile_Document`.`id` 
			))) 
WHERE
	(
	0 <> COALESCE (( `DocumentType_documenttype_id_Typology`.`finalclass` = 'DocumentType' ), 1 ))
```

