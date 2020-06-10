| 列                            | 类型                               | 注释 |
| :---------------------------- | ---------------------------------- | ---- |
| id                            | int [**0**]                        |      |
| document_id                   | int *NULL* [**0**]                 |      |
| document_name                 | varchar(255) *NULL* []             |      |
| error_id                      | int *NULL* [**0**]                 |      |
| error_name                    | varchar(255) *NULL* []             |      |
| link_type                     | varchar(255) *NULL* []             |      |
| friendlyname                  | varchar(255) *NULL*                |      |
| document_id_friendlyname      | varchar(255) *NULL*                |      |
| document_id_finalclass_recall | varchar(255) *NULL* [**Document**] |      |
| document_id_obsolescence_flag | int [**0**]                        |      |
| error_id_friendlyname         | varchar(255) *NULL*                |      |

```
SELECT DISTINCT
	`lnkDocumentToError`.`link_id` AS `id`,
	`lnkDocumentToError`.`document_id` AS `document_id`,
	`Document_document_id`.`name` AS `document_name`,
	`lnkDocumentToError`.`error_id` AS `error_id`,
	`KnownError_error_id`.`name` AS `error_name`,
	`lnkDocumentToError`.`link_type` AS `link_type`,
	cast( concat( COALESCE ( `lnkDocumentToError`.`link_type`, '' )) AS CHAR charset utf8mb4 ) AS `friendlyname`,
IF
	((
			`Document_document_id`.`finalclass` = 'Document' 
			),
		cast( concat( COALESCE ( 'Document', '' )) AS CHAR charset utf8mb4 ),
	cast( concat( COALESCE ( `Document_document_id`.`name`, '' )) AS CHAR charset utf8mb4 )) AS `document_id_friendlyname`,
	`Document_document_id`.`finalclass` AS `document_id_finalclass_recall`,
	COALESCE (( `Document_document_id`.`status` = 'obsolete' ), 0 ) AS `document_id_obsolescence_flag`,
	cast( concat( COALESCE ( `KnownError_error_id`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `error_id_friendlyname` 
FROM
	((
			`lnkdocumenttoerror` `lnkDocumentToError`
			JOIN `document` `Document_document_id` ON ((
					`lnkDocumentToError`.`document_id` = `Document_document_id`.`id` 
				)))
		JOIN `knownerror` `KnownError_error_id` ON ((
				`lnkDocumentToError`.`error_id` = `KnownError_error_id`.`id` 
			))) 
WHERE
	(
	0 <> 1)
```

