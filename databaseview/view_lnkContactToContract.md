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
select distinct `lnkContactToContract`.`id` AS `id`,`lnkContactToContract`.`contract_id` AS `contract_id`,`Contract_contract_id`.`name` AS `contract_name`,`lnkContactToContract`.`contact_id` AS `contact_id`,`Contact_contact_id`.`name` AS `contact_name`,cast(concat(coalesce(`lnkContactToContract`.`contract_id`,''),coalesce(' ',''),coalesce(`lnkContactToContract`.`contact_id`,'')) as char charset utf8mb4) AS `friendlyname`,cast(concat(coalesce(`Contract_contract_id`.`name`,'')) as char charset utf8mb4) AS `contract_id_friendlyname`,`Contract_contract_id`.`finalclass` AS `contract_id_finalclass_recall`,if((`Contact_contact_id`.`finalclass` in ('Team','Contact')),cast(concat(coalesce(`Contact_contact_id`.`name`,'')) as char charset utf8mb4),cast(concat(coalesce(`Contact_contact_id_poly_Person`.`first_name`,''),coalesce(' ',''),coalesce(`Contact_contact_id`.`name`,'')) as char charset utf8mb4)) AS `contact_id_friendlyname`,`Contact_contact_id`.`finalclass` AS `contact_id_finalclass_recall`,coalesce((`Contact_contact_id`.`status` = 'inactive'),0) AS `contact_id_obsolescence_flag` from ((`lnkcontacttocontract` `lnkContactToContract` join `contract` `Contract_contract_id` on((`lnkContactToContract`.`contract_id` = `Contract_contract_id`.`id`))) join (`contact` `Contact_contact_id` left join `person` `Contact_contact_id_poly_Person` on((`Contact_contact_id`.`id` = `Contact_contact_id_poly_Person`.`id`))) on((`lnkContactToContract`.`contact_id` = `Contact_contact_id`.`id`))) where (0 <> 1)
```

