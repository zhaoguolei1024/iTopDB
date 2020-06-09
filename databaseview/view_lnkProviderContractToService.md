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
select distinct `lnkProviderContractToService`.`id` AS `id`,`lnkProviderContractToService`.`service_id` AS `service_id`,`Service_service_id`.`name` AS `service_name`,`lnkProviderContractToService`.`providercontract_id` AS `providercontract_id`,`ProviderContract_providercontract_id_Contract`.`name` AS `providercontract_name`,cast(concat(coalesce(`lnkProviderContractToService`.`service_id`,''),coalesce(' ',''),coalesce(`lnkProviderContractToService`.`providercontract_id`,'')) as char charset utf8mb4) AS `friendlyname`,cast(concat(coalesce(`Service_service_id`.`name`,'')) as char charset utf8mb4) AS `service_id_friendlyname`,cast(concat(coalesce(`ProviderContract_providercontract_id_Contract`.`name`,'')) as char charset utf8mb4) AS `providercontract_id_friendlyname` from ((`lnkprovidercontracttoservice` `lnkProviderContractToService` join `service` `Service_service_id` on((`lnkProviderContractToService`.`service_id` = `Service_service_id`.`id`))) join `contract` `ProviderContract_providercontract_id_Contract` on((`lnkProviderContractToService`.`providercontract_id` = `ProviderContract_providercontract_id_Contract`.`id`))) where (0 <> coalesce((`ProviderContract_providercontract_id_Contract`.`finalclass` = 'ProviderContract'),1))
```

