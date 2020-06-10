| 列                            | 类型                                                  | 注释 |
| :---------------------------- | ----------------------------------------------------- | ---- |
| id                            | int [**0**]                                           |      |
| name                          | varchar(255) *NULL* []                                |      |
| org_id                        | int *NULL* [**0**]                                    |      |
| organization_name             | varchar(255) *NULL* []                                |      |
| description                   | text *NULL*                                           |      |
| start_date                    | date *NULL*                                           |      |
| end_date                      | date *NULL*                                           |      |
| cost                          | varchar(255) *NULL* []                                |      |
| cost_currency                 | enum('dollars','euros') *NULL*                        |      |
| contracttype_id               | int *NULL* [**0**]                                    |      |
| contracttype_name             | varchar(255) *NULL* []                                |      |
| billing_frequency             | varchar(255) *NULL* []                                |      |
| cost_unit                     | varchar(255) *NULL* []                                |      |
| provider_id                   | int *NULL* [**0**]                                    |      |
| provider_name                 | varchar(255) *NULL* []                                |      |
| status                        | enum('implementation','obsolete','production') *NULL* |      |
| sla                           | varchar(255) *NULL* []                                |      |
| coverage                      | varchar(255) *NULL* []                                |      |
| finalclass                    | varchar(255) *NULL* [**Contract**]                    |      |
| friendlyname                  | varchar(255) *NULL*                                   |      |
| org_id_friendlyname           | varchar(255) *NULL*                                   |      |
| org_id_obsolescence_flag      | int [**0**]                                           |      |
| contracttype_id_friendlyname  | varchar(255) *NULL*                                   |      |
| provider_id_friendlyname      | varchar(255) *NULL*                                   |      |
| provider_id_obsolescence_flag | int [**0**]                                           |      |

```
SELECT DISTINCT
	`ProviderContract`.`id` AS `id`,
	`ProviderContract_Contract`.`name` AS `name`,
	`ProviderContract_Contract`.`org_id` AS `org_id`,
	`Organization_org_id`.`name` AS `organization_name`,
	`ProviderContract_Contract`.`description` AS `description`,
	`ProviderContract_Contract`.`start_date` AS `start_date`,
	`ProviderContract_Contract`.`end_date` AS `end_date`,
	`ProviderContract_Contract`.`cost` AS `cost`,
	`ProviderContract_Contract`.`cost_currency` AS `cost_currency`,
	`ProviderContract_Contract`.`contracttype_id` AS `contracttype_id`,
	`ContractType_contracttype_id_Typology`.`name` AS `contracttype_name`,
	`ProviderContract_Contract`.`billing_frequency` AS `billing_frequency`,
	`ProviderContract_Contract`.`cost_unit` AS `cost_unit`,
	`ProviderContract_Contract`.`provider_id` AS `provider_id`,
	`Organization_provider_id`.`name` AS `provider_name`,
	`ProviderContract_Contract`.`status` AS `status`,
	`ProviderContract`.`sla` AS `sla`,
	`ProviderContract`.`coverage` AS `coverage`,
	`ProviderContract_Contract`.`finalclass` AS `finalclass`,
	cast( concat( COALESCE ( `ProviderContract_Contract`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `friendlyname`,
	cast( concat( COALESCE ( `Organization_org_id`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `org_id_friendlyname`,
	COALESCE (( `Organization_org_id`.`status` = 'inactive' ), 0 ) AS `org_id_obsolescence_flag`,
	cast( concat( COALESCE ( `ContractType_contracttype_id_Typology`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `contracttype_id_friendlyname`,
	cast( concat( COALESCE ( `Organization_provider_id`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `provider_id_friendlyname`,
	COALESCE (( `Organization_provider_id`.`status` = 'inactive' ), 0 ) AS `provider_id_obsolescence_flag` 
FROM
	(
		`providercontract` `ProviderContract`
		JOIN (((
					`contract` `ProviderContract_Contract`
					JOIN `organization` `Organization_org_id` ON ((
							`ProviderContract_Contract`.`org_id` = `Organization_org_id`.`id` 
						)))
				LEFT JOIN `typology` `ContractType_contracttype_id_Typology` ON ((
						`ProviderContract_Contract`.`contracttype_id` = `ContractType_contracttype_id_Typology`.`id` 
					)))
			JOIN `organization` `Organization_provider_id` ON ((
					`ProviderContract_Contract`.`provider_id` = `Organization_provider_id`.`id` 
					))) ON ((
				`ProviderContract`.`id` = `ProviderContract_Contract`.`id` 
			))) 
WHERE
	(
	0 <> COALESCE (( `ContractType_contracttype_id_Typology`.`finalclass` = 'ContractType' ), 1 ))
```

