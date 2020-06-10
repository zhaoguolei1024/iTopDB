| 列                            | 类型                               | 注释 |
| :---------------------------- | ---------------------------------- | ---- |
| id                            | int [**0**]                        |      |
| software_id                   | int *NULL* [**0**]                 |      |
| software_name                 | varchar(255) *NULL* []             |      |
| document_id                   | int *NULL* [**0**]                 |      |
| document_name                 | varchar(255) *NULL* []             |      |
| friendlyname                  | varchar(23) *NULL*                 |      |
| software_id_friendlyname      | varchar(511) *NULL*                |      |
| document_id_friendlyname      | varchar(255) *NULL*                |      |
| document_id_finalclass_recall | varchar(255) *NULL* [**Document**] |      |
| document_id_obsolescence_flag | int [**0**]                        |      |

```
SELECT DISTINCT
	`lnkDocumentToSoftware`.`id` AS `id`,
	`lnkDocumentToSoftware`.`software_id` AS `software_id`,
	`Software_software_id`.`name` AS `software_name`,
	`lnkDocumentToSoftware`.`document_id` AS `document_id`,
	`Document_document_id`.`name` AS `document_name`,
	cast(
		concat(
			COALESCE ( `lnkDocumentToSoftware`.`software_id`, '' ),
			COALESCE ( ' ', '' ),
		COALESCE ( `lnkDocumentToSoftware`.`document_id`, '' )) AS CHAR charset utf8mb4 
	) AS `friendlyname`,
	cast(
		concat(
			COALESCE ( `Software_software_id`.`name`, '' ),
			COALESCE ( ' ', '' ),
		COALESCE ( `Software_software_id`.`version`, '' )) AS CHAR charset utf8mb4 
	) AS `software_id_friendlyname`,
IF
	((
			`Document_document_id`.`finalclass` = 'Document' 
			),
		cast( concat( COALESCE ( 'Document', '' )) AS CHAR charset utf8mb4 ),
	cast( concat( COALESCE ( `Document_document_id`.`name`, '' )) AS CHAR charset utf8mb4 )) AS `document_id_friendlyname`,
	`Document_document_id`.`finalclass` AS `document_id_finalclass_recall`,
	COALESCE (( `Document_document_id`.`status` = 'obsolete' ), 0 ) AS `document_id_obsolescence_flag` 
FROM
	((
			`lnkdocumenttosoftware` `lnkDocumentToSoftware`
			JOIN `software` `Software_software_id` ON ((
					`lnkDocumentToSoftware`.`software_id` = `Software_software_id`.`id` 
				)))
		JOIN `document` `Document_document_id` ON ((
				`lnkDocumentToSoftware`.`document_id` = `Document_document_id`.`id` 
			))) 
WHERE
	(
	0 <> 1)
```

