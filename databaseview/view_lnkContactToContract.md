| 列                            | 类型                               | 注释 |
| :---------------------------- | ---------------------------------- | ---- |
| id                            | int [**0**]                        |      |
| contract_id                   | int *NULL* [**0**]                 |      |
| contract_name                 | varchar(255) *NULL* []             |      |
| contact_id                    | int *NULL* [**0**]                 |      |
| contact_name                  | varchar(255) *NULL* []             |      |
| friendlyname                  | varchar(23) *NULL*                 |      |
| contract_id_friendlyname      | varchar(255) *NULL*                |      |
| contract_id_finalclass_recall | varchar(255) *NULL* [**Contract**] |      |
| contact_id_friendlyname       | varchar(511) *NULL*                |      |
| contact_id_finalclass_recall  | varchar(255) *NULL* [**Contact**]  |      |
| contact_id_obsolescence_flag  | int [**0**]                        |      |

```
SELECT DISTINCT
	`lnkContactToContract`.`id` AS `id`,
	`lnkContactToContract`.`contract_id` AS `contract_id`,
	`Contract_contract_id`.`name` AS `contract_name`,
	`lnkContactToContract`.`contact_id` AS `contact_id`,
	`Contact_contact_id`.`name` AS `contact_name`,
	cast(
		concat(
			COALESCE ( `lnkContactToContract`.`contract_id`, '' ),
			COALESCE ( ' ', '' ),
		COALESCE ( `lnkContactToContract`.`contact_id`, '' )) AS CHAR charset utf8mb4 
	) AS `friendlyname`,
	cast( concat( COALESCE ( `Contract_contract_id`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `contract_id_friendlyname`,
	`Contract_contract_id`.`finalclass` AS `contract_id_finalclass_recall`,
IF
	((
			`Contact_contact_id`.`finalclass` IN ( 'Team', 'Contact' )),
		cast( concat( COALESCE ( `Contact_contact_id`.`name`, '' )) AS CHAR charset utf8mb4 ),
		cast(
			concat(
				COALESCE ( `Contact_contact_id_poly_Person`.`first_name`, '' ),
				COALESCE ( ' ', '' ),
			COALESCE ( `Contact_contact_id`.`name`, '' )) AS CHAR charset utf8mb4 
		)) AS `contact_id_friendlyname`,
	`Contact_contact_id`.`finalclass` AS `contact_id_finalclass_recall`,
	COALESCE (( `Contact_contact_id`.`status` = 'inactive' ), 0 ) AS `contact_id_obsolescence_flag` 
FROM
	((
			`lnkcontacttocontract` `lnkContactToContract`
			JOIN `contract` `Contract_contract_id` ON ((
					`lnkContactToContract`.`contract_id` = `Contract_contract_id`.`id` 
				)))
		JOIN (
			`contact` `Contact_contact_id`
			LEFT JOIN `person` `Contact_contact_id_poly_Person` ON ((
					`Contact_contact_id`.`id` = `Contact_contact_id_poly_Person`.`id` 
					))) ON ((
				`lnkContactToContract`.`contact_id` = `Contact_contact_id`.`id` 
			))) 
WHERE
	(
	0 <> 1)
```

