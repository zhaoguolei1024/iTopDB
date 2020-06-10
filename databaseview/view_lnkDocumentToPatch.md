| 列                            | 类型                               | 注释 |
| :---------------------------- | ---------------------------------- | ---- |
| id                            | int [**0**]                        |      |
| patch_id                      | int *NULL* [**0**]                 |      |
| patch_name                    | varchar(255) *NULL* []             |      |
| document_id                   | int *NULL* [**0**]                 |      |
| document_name                 | varchar(255) *NULL* []             |      |
| friendlyname                  | varchar(23) *NULL*                 |      |
| patch_id_friendlyname         | varchar(255) *NULL*                |      |
| patch_id_finalclass_recall    | varchar(255) *NULL* [**Patch**]    |      |
| document_id_friendlyname      | varchar(255) *NULL*                |      |
| document_id_finalclass_recall | varchar(255) *NULL* [**Document**] |      |
| document_id_obsolescence_flag | int [**0**]                        |      |

```
SELECT DISTINCT
	`lnkDocumentToPatch`.`id` AS `id`,
	`lnkDocumentToPatch`.`patch_id` AS `patch_id`,
	`Patch_patch_id`.`name` AS `patch_name`,
	`lnkDocumentToPatch`.`document_id` AS `document_id`,
	`Document_document_id`.`name` AS `document_name`,
	cast(
		concat(
			COALESCE ( `lnkDocumentToPatch`.`patch_id`, '' ),
			COALESCE ( ' ', '' ),
		COALESCE ( `lnkDocumentToPatch`.`document_id`, '' )) AS CHAR charset utf8mb4 
	) AS `friendlyname`,
	cast( concat( COALESCE ( `Patch_patch_id`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `patch_id_friendlyname`,
	`Patch_patch_id`.`finalclass` AS `patch_id_finalclass_recall`,
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
			`lnkdocumenttopatch` `lnkDocumentToPatch`
			JOIN `patch` `Patch_patch_id` ON ((
					`lnkDocumentToPatch`.`patch_id` = `Patch_patch_id`.`id` 
				)))
		JOIN `document` `Document_document_id` ON ((
				`lnkDocumentToPatch`.`document_id` = `Document_document_id`.`id` 
			))) 
WHERE
	(
	0 <> 1)
```

