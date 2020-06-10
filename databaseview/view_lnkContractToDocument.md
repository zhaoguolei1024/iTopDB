| 列                            | 类型                               | 注释 |
| :---------------------------- | ---------------------------------- | ---- |
| id                            | int [**0**]                        |      |
| contract_id                   | int *NULL* [**0**]                 |      |
| contract_name                 | varchar(255) *NULL* []             |      |
| document_id                   | int *NULL* [**0**]                 |      |
| document_name                 | varchar(255) *NULL* []             |      |
| friendlyname                  | varchar(23) *NULL*                 |      |
| contract_id_friendlyname      | varchar(255) *NULL*                |      |
| contract_id_finalclass_recall | varchar(255) *NULL* [**Contract**] |      |
| document_id_friendlyname      | varchar(255) *NULL*                |      |
| document_id_finalclass_recall | varchar(255) *NULL* [**Document**] |      |
| document_id_obsolescence_flag | int [**0**]                        |      |

```
SELECT DISTINCT
	`lnkContractToDocument`.`id` AS `id`,
	`lnkContractToDocument`.`contract_id` AS `contract_id`,
	`Contract_contract_id`.`name` AS `contract_name`,
	`lnkContractToDocument`.`document_id` AS `document_id`,
	`Document_document_id`.`name` AS `document_name`,
	cast(
		concat(
			COALESCE ( `lnkContractToDocument`.`contract_id`, '' ),
			COALESCE ( ' ', '' ),
		COALESCE ( `lnkContractToDocument`.`document_id`, '' )) AS CHAR charset utf8mb4 
	) AS `friendlyname`,
	cast( concat( COALESCE ( `Contract_contract_id`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `contract_id_friendlyname`,
	`Contract_contract_id`.`finalclass` AS `contract_id_finalclass_recall`,
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
			`lnkcontracttodocument` `lnkContractToDocument`
			JOIN `contract` `Contract_contract_id` ON ((
					`lnkContractToDocument`.`contract_id` = `Contract_contract_id`.`id` 
				)))
		JOIN `document` `Document_document_id` ON ((
				`lnkContractToDocument`.`document_id` = `Document_document_id`.`id` 
			))) 
WHERE
	(
	0 <> 1)
```

