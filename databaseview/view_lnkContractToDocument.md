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
select distinct `lnkContractToDocument`.`id` AS `id`,`lnkContractToDocument`.`contract_id` AS `contract_id`,`Contract_contract_id`.`name` AS `contract_name`,`lnkContractToDocument`.`document_id` AS `document_id`,`Document_document_id`.`name` AS `document_name`,cast(concat(coalesce(`lnkContractToDocument`.`contract_id`,''),coalesce(' ',''),coalesce(`lnkContractToDocument`.`document_id`,'')) as char charset utf8mb4) AS `friendlyname`,cast(concat(coalesce(`Contract_contract_id`.`name`,'')) as char charset utf8mb4) AS `contract_id_friendlyname`,`Contract_contract_id`.`finalclass` AS `contract_id_finalclass_recall`,if((`Document_document_id`.`finalclass` = 'Document'),cast(concat(coalesce('Document','')) as char charset utf8mb4),cast(concat(coalesce(`Document_document_id`.`name`,'')) as char charset utf8mb4)) AS `document_id_friendlyname`,`Document_document_id`.`finalclass` AS `document_id_finalclass_recall`,coalesce((`Document_document_id`.`status` = 'obsolete'),0) AS `document_id_obsolescence_flag` from ((`lnkcontracttodocument` `lnkContractToDocument` join `contract` `Contract_contract_id` on((`lnkContractToDocument`.`contract_id` = `Contract_contract_id`.`id`))) join `document` `Document_document_id` on((`lnkContractToDocument`.`document_id` = `Document_document_id`.`id`))) where (0 <> 1)
```

