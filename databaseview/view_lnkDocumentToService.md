| 列                            | 类型                               | 注释 |
| :---------------------------- | ---------------------------------- | ---- |
| id                            | int [**0**]                        |      |
| service_id                    | int *NULL* [**0**]                 |      |
| service_name                  | varchar(255) *NULL* []             |      |
| document_id                   | int *NULL* [**0**]                 |      |
| document_name                 | varchar(255) *NULL* []             |      |
| friendlyname                  | varchar(23) *NULL*                 |      |
| service_id_friendlyname       | varchar(255) *NULL*                |      |
| document_id_friendlyname      | varchar(255) *NULL*                |      |
| document_id_finalclass_recall | varchar(255) *NULL* [**Document**] |      |
| document_id_obsolescence_flag | int [**0**]                        |      |

```
SELECT DISTINCT
	`lnkDocumentToService`.`id` AS `id`,
	`lnkDocumentToService`.`service_id` AS `service_id`,
	`Service_service_id`.`name` AS `service_name`,
	`lnkDocumentToService`.`document_id` AS `document_id`,
	`Document_document_id`.`name` AS `document_name`,
	cast(
		concat(
			COALESCE ( `lnkDocumentToService`.`service_id`, '' ),
			COALESCE ( ' ', '' ),
		COALESCE ( `lnkDocumentToService`.`document_id`, '' )) AS CHAR charset utf8mb4 
	) AS `friendlyname`,
	cast( concat( COALESCE ( `Service_service_id`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `service_id_friendlyname`,
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
			`lnkdocumenttoservice` `lnkDocumentToService`
			JOIN `service` `Service_service_id` ON ((
					`lnkDocumentToService`.`service_id` = `Service_service_id`.`id` 
				)))
		JOIN `document` `Document_document_id` ON ((
				`lnkDocumentToService`.`document_id` = `Document_document_id`.`id` 
			))) 
WHERE
	(
	0 <> 1)
```

