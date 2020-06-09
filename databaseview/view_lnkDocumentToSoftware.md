| 列                            | 类型                               | 注释 |
| :---------------------------- | ---------------------------------- | ---- |
| id                            | int [**0**]                        |      |
| software_id                   | int *NULL* [**0**]                 |      |
| software_name                 | varchar(255) *NULL* []             |      |
| document_id                   | int *NULL* [**0**]                 |      |
| document_name                 | varchar(255) *NULL* []             |      |
| friendlyname                  | varchar(23) *NULL*                 |      |
| software_id_friendlyname      | varchar(511) *NULL*                |      |
| document_id_friendlyname      | varchar(255) *NULL*                |      |
| document_id_finalclass_recall | varchar(255) *NULL* [**Document**] |      |
| document_id_obsolescence_flag | int [**0**]                        |      |

```
select distinct `lnkDocumentToSoftware`.`id` AS `id`,`lnkDocumentToSoftware`.`software_id` AS `software_id`,`Software_software_id`.`name` AS `software_name`,`lnkDocumentToSoftware`.`document_id` AS `document_id`,`Document_document_id`.`name` AS `document_name`,cast(concat(coalesce(`lnkDocumentToSoftware`.`software_id`,''),coalesce(' ',''),coalesce(`lnkDocumentToSoftware`.`document_id`,'')) as char charset utf8mb4) AS `friendlyname`,cast(concat(coalesce(`Software_software_id`.`name`,''),coalesce(' ',''),coalesce(`Software_software_id`.`version`,'')) as char charset utf8mb4) AS `software_id_friendlyname`,if((`Document_document_id`.`finalclass` = 'Document'),cast(concat(coalesce('Document','')) as char charset utf8mb4),cast(concat(coalesce(`Document_document_id`.`name`,'')) as char charset utf8mb4)) AS `document_id_friendlyname`,`Document_document_id`.`finalclass` AS `document_id_finalclass_recall`,coalesce((`Document_document_id`.`status` = 'obsolete'),0) AS `document_id_obsolescence_flag` from ((`lnkdocumenttosoftware` `lnkDocumentToSoftware` join `software` `Software_software_id` on((`lnkDocumentToSoftware`.`software_id` = `Software_software_id`.`id`))) join `document` `Document_document_id` on((`lnkDocumentToSoftware`.`document_id` = `Document_document_id`.`id`))) where (0 <> 1)
```

