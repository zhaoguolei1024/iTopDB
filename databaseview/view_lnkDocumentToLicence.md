| 列                            | 类型                               | 注释 |
| :---------------------------- | ---------------------------------- | ---- |
| id                            | int [**0**]                        |      |
| licence_id                    | int *NULL* [**0**]                 |      |
| licence_name                  | varchar(255) *NULL* []             |      |
| document_id                   | int *NULL* [**0**]                 |      |
| document_name                 | varchar(255) *NULL* []             |      |
| friendlyname                  | varchar(23) *NULL*                 |      |
| licence_id_friendlyname       | varchar(255) *NULL*                |      |
| licence_id_finalclass_recall  | varchar(255) *NULL* [**Licence**]  |      |
| licence_id_obsolescence_flag  | int [**0**]                        |      |
| document_id_friendlyname      | varchar(255) *NULL*                |      |
| document_id_finalclass_recall | varchar(255) *NULL* [**Document**] |      |
| document_id_obsolescence_flag | int [**0**]                        |      |

```
SELECT DISTINCT
	`lnkDocumentToLicence`.`id` AS `id`,
	`lnkDocumentToLicence`.`licence_id` AS `licence_id`,
	`Licence_licence_id`.`name` AS `licence_name`,
	`lnkDocumentToLicence`.`document_id` AS `document_id`,
	`Document_document_id`.`name` AS `document_name`,
	cast(
		concat(
			COALESCE ( `lnkDocumentToLicence`.`licence_id`, '' ),
			COALESCE ( ' ', '' ),
		COALESCE ( `lnkDocumentToLicence`.`document_id`, '' )) AS CHAR charset utf8mb4 
	) AS `friendlyname`,
	cast( concat( COALESCE ( `Licence_licence_id`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `licence_id_friendlyname`,
	`Licence_licence_id`.`finalclass` AS `licence_id_finalclass_recall`,
	COALESCE (((
				`Licence_licence_id`.`perpetual` = 'no' 
				) 
			AND (( `Licence_licence_id`.`end_date` IS NULL ) = 0 ) 
			AND (
			`Licence_licence_id`.`end_date` < date_format(( now() - INTERVAL 15 MONTH ), '%Y-%m-%d 00:00:00' ))),
		0 
	) AS `licence_id_obsolescence_flag`,
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
			`lnkdocumenttolicence` `lnkDocumentToLicence`
			JOIN `licence` `Licence_licence_id` ON ((
					`lnkDocumentToLicence`.`licence_id` = `Licence_licence_id`.`id` 
				)))
		JOIN `document` `Document_document_id` ON ((
				`lnkDocumentToLicence`.`document_id` = `Document_document_id`.`id` 
			))) 
WHERE
	(
	0 <> 1)
```

