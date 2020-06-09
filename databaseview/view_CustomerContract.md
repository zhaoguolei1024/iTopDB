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
| finalclass                    | varchar(255) *NULL* [**Contract**]                    |      |
| friendlyname                  | varchar(255) *NULL*                                   |      |
| org_id_friendlyname           | varchar(255) *NULL*                                   |      |
| org_id_obsolescence_flag      | int [**0**]                                           |      |
| contracttype_id_friendlyname  | varchar(255) *NULL*                                   |      |
| provider_id_friendlyname      | varchar(255) *NULL*                                   |      |
| provider_id_obsolescence_flag | int [**0**]                                           |      |

```
select distinct `CustomerContract_Contract`.`id` AS `id`,`CustomerContract_Contract`.`name` AS `name`,`CustomerContract_Contract`.`org_id` AS `org_id`,`Organization_org_id`.`name` AS `organization_name`,`CustomerContract_Contract`.`description` AS `description`,`CustomerContract_Contract`.`start_date` AS `start_date`,`CustomerContract_Contract`.`end_date` AS `end_date`,`CustomerContract_Contract`.`cost` AS `cost`,`CustomerContract_Contract`.`cost_currency` AS `cost_currency`,`CustomerContract_Contract`.`contracttype_id` AS `contracttype_id`,`ContractType_contracttype_id_Typology`.`name` AS `contracttype_name`,`CustomerContract_Contract`.`billing_frequency` AS `billing_frequency`,`CustomerContract_Contract`.`cost_unit` AS `cost_unit`,`CustomerContract_Contract`.`provider_id` AS `provider_id`,`Organization_provider_id`.`name` AS `provider_name`,`CustomerContract_Contract`.`status` AS `status`,`CustomerContract_Contract`.`finalclass` AS `finalclass`,cast(concat(coalesce(`CustomerContract_Contract`.`name`,'')) as char charset utf8mb4) AS `friendlyname`,cast(concat(coalesce(`Organization_org_id`.`name`,'')) as char charset utf8mb4) AS `org_id_friendlyname`,coalesce((`Organization_org_id`.`status` = 'inactive'),0) AS `org_id_obsolescence_flag`,cast(concat(coalesce(`ContractType_contracttype_id_Typology`.`name`,'')) as char charset utf8mb4) AS `contracttype_id_friendlyname`,cast(concat(coalesce(`Organization_provider_id`.`name`,'')) as char charset utf8mb4) AS `provider_id_friendlyname`,coalesce((`Organization_provider_id`.`status` = 'inactive'),0) AS `provider_id_obsolescence_flag` from (((`contract` `CustomerContract_Contract` join `organization` `Organization_org_id` on((`CustomerContract_Contract`.`org_id` = `Organization_org_id`.`id`))) left join `typology` `ContractType_contracttype_id_Typology` on((`CustomerContract_Contract`.`contracttype_id` = `ContractType_contracttype_id_Typology`.`id`))) join `organization` `Organization_provider_id` on((`CustomerContract_Contract`.`provider_id` = `Organization_provider_id`.`id`))) where ((0 <> coalesce((`ContractType_contracttype_id_Typology`.`finalclass` = 'ContractType'),1)) and (0 <> coalesce((`CustomerContract_Contract`.`finalclass` = 'CustomerContract'),1)))
```

