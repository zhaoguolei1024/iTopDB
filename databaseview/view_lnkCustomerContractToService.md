| 列                               | 类型                   | 注释 |
| :------------------------------- | ---------------------- | ---- |
| id                               | int [**0**]            |      |
| customercontract_id              | int *NULL* [**0**]     |      |
| customercontract_name            | varchar(255) *NULL* [] |      |
| service_id                       | int *NULL* [**0**]     |      |
| service_name                     | varchar(255) *NULL* [] |      |
| sla_id                           | int *NULL* [**0**]     |      |
| sla_name                         | varchar(255) *NULL* [] |      |
| friendlyname                     | varchar(23) *NULL*     |      |
| customercontract_id_friendlyname | varchar(255) *NULL*    |      |
| service_id_friendlyname          | varchar(255) *NULL*    |      |
| sla_id_friendlyname              | varchar(255) *NULL*    |      |

```
SELECT DISTINCT
	`lnkCustomerContractToService`.`id` AS `id`,
	`lnkCustomerContractToService`.`customercontract_id` AS `customercontract_id`,
	`CustomerContract_customercontract_id_Contract`.`name` AS `customercontract_name`,
	`lnkCustomerContractToService`.`service_id` AS `service_id`,
	`Service_service_id`.`name` AS `service_name`,
	`lnkCustomerContractToService`.`sla_id` AS `sla_id`,
	`SLA_sla_id`.`name` AS `sla_name`,
	cast(
		concat(
			COALESCE ( `lnkCustomerContractToService`.`customercontract_id`, '' ),
			COALESCE ( ' ', '' ),
		COALESCE ( `lnkCustomerContractToService`.`service_id`, '' )) AS CHAR charset utf8mb4 
	) AS `friendlyname`,
	cast( concat( COALESCE ( `CustomerContract_customercontract_id_Contract`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `customercontract_id_friendlyname`,
	cast( concat( COALESCE ( `Service_service_id`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `service_id_friendlyname`,
	cast( concat( COALESCE ( `SLA_sla_id`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `sla_id_friendlyname` 
FROM
	(((
				`lnkcustomercontracttoservice` `lnkCustomerContractToService`
				JOIN `contract` `CustomerContract_customercontract_id_Contract` ON ((
						`lnkCustomerContractToService`.`customercontract_id` = `CustomerContract_customercontract_id_Contract`.`id` 
					)))
			JOIN `service` `Service_service_id` ON ((
					`lnkCustomerContractToService`.`service_id` = `Service_service_id`.`id` 
				)))
		LEFT JOIN `sla` `SLA_sla_id` ON ((
				`lnkCustomerContractToService`.`sla_id` = `SLA_sla_id`.`id` 
			))) 
WHERE
	(
	0 <> COALESCE (( `CustomerContract_customercontract_id_Contract`.`finalclass` = 'CustomerContract' ), 1 ))
```

