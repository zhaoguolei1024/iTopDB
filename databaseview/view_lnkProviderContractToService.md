| 列                               | 类型                   | 注释 |
| :------------------------------- | ---------------------- | ---- |
| id                               | int [**0**]            |      |
| service_id                       | int *NULL* [**0**]     |      |
| service_name                     | varchar(255) *NULL* [] |      |
| providercontract_id              | int *NULL* [**0**]     |      |
| providercontract_name            | varchar(255) *NULL* [] |      |
| friendlyname                     | varchar(23) *NULL*     |      |
| service_id_friendlyname          | varchar(255) *NULL*    |      |
| providercontract_id_friendlyname | varchar(255) *NULL*    |      |

```
SELECT DISTINCT
	`lnkProviderContractToService`.`id` AS `id`,
	`lnkProviderContractToService`.`service_id` AS `service_id`,
	`Service_service_id`.`name` AS `service_name`,
	`lnkProviderContractToService`.`providercontract_id` AS `providercontract_id`,
	`ProviderContract_providercontract_id_Contract`.`name` AS `providercontract_name`,
	cast(
		concat(
			COALESCE ( `lnkProviderContractToService`.`service_id`, '' ),
			COALESCE ( ' ', '' ),
		COALESCE ( `lnkProviderContractToService`.`providercontract_id`, '' )) AS CHAR charset utf8mb4 
	) AS `friendlyname`,
	cast( concat( COALESCE ( `Service_service_id`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `service_id_friendlyname`,
	cast( concat( COALESCE ( `ProviderContract_providercontract_id_Contract`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `providercontract_id_friendlyname` 
FROM
	((
			`lnkprovidercontracttoservice` `lnkProviderContractToService`
			JOIN `service` `Service_service_id` ON ((
					`lnkProviderContractToService`.`service_id` = `Service_service_id`.`id` 
				)))
		JOIN `contract` `ProviderContract_providercontract_id_Contract` ON ((
				`lnkProviderContractToService`.`providercontract_id` = `ProviderContract_providercontract_id_Contract`.`id` 
			))) 
WHERE
	(
	0 <> COALESCE (( `ProviderContract_providercontract_id_Contract`.`finalclass` = 'ProviderContract' ), 1 ))
```

