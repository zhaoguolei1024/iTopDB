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
select distinct `lnkCustomerContractToService`.`id` AS `id`,`lnkCustomerContractToService`.`customercontract_id` AS `customercontract_id`,`CustomerContract_customercontract_id_Contract`.`name` AS `customercontract_name`,`lnkCustomerContractToService`.`service_id` AS `service_id`,`Service_service_id`.`name` AS `service_name`,`lnkCustomerContractToService`.`sla_id` AS `sla_id`,`SLA_sla_id`.`name` AS `sla_name`,cast(concat(coalesce(`lnkCustomerContractToService`.`customercontract_id`,''),coalesce(' ',''),coalesce(`lnkCustomerContractToService`.`service_id`,'')) as char charset utf8mb4) AS `friendlyname`,cast(concat(coalesce(`CustomerContract_customercontract_id_Contract`.`name`,'')) as char charset utf8mb4) AS `customercontract_id_friendlyname`,cast(concat(coalesce(`Service_service_id`.`name`,'')) as char charset utf8mb4) AS `service_id_friendlyname`,cast(concat(coalesce(`SLA_sla_id`.`name`,'')) as char charset utf8mb4) AS `sla_id_friendlyname` from (((`lnkcustomercontracttoservice` `lnkCustomerContractToService` join `contract` `CustomerContract_customercontract_id_Contract` on((`lnkCustomerContractToService`.`customercontract_id` = `CustomerContract_customercontract_id_Contract`.`id`))) join `service` `Service_service_id` on((`lnkCustomerContractToService`.`service_id` = `Service_service_id`.`id`))) left join `sla` `SLA_sla_id` on((`lnkCustomerContractToService`.`sla_id` = `SLA_sla_id`.`id`))) where (0 <> coalesce((`CustomerContract_customercontract_id_Contract`.`finalclass` = 'CustomerContract'),1))
```

