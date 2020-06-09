| 列                            | 类型                               | 注释 |
| :---------------------------- | ---------------------------------- | ---- |
| id                            | int [**0**]                        |      |
| service_id                    | int *NULL* [**0**]                 |      |
| service_name                  | varchar(255) *NULL* []             |      |
| document_id                   | int *NULL* [**0**]                 |      |
| document_name                 | varchar(255) *NULL* []             |      |
| friendlyname                  | varchar(23) *NULL*                 |      |
| service_id_friendlyname       | varchar(255) *NULL*                |      |
| document_id_friendlyname      | varchar(255) *NULL*                |      |
| document_id_finalclass_recall | varchar(255) *NULL* [**Document**] |      |
| document_id_obsolescence_flag | int [**0**]                        |      |

```
select distinct `lnkDocumentToService`.`id` AS `id`,`lnkDocumentToService`.`service_id` AS `service_id`,`Service_service_id`.`name` AS `service_name`,`lnkDocumentToService`.`document_id` AS `document_id`,`Document_document_id`.`name` AS `document_name`,cast(concat(coalesce(`lnkDocumentToService`.`service_id`,''),coalesce(' ',''),coalesce(`lnkDocumentToService`.`document_id`,'')) as char charset utf8mb4) AS `friendlyname`,cast(concat(coalesce(`Service_service_id`.`name`,'')) as char charset utf8mb4) AS `service_id_friendlyname`,if((`Document_document_id`.`finalclass` = 'Document'),cast(concat(coalesce('Document','')) as char charset utf8mb4),cast(concat(coalesce(`Document_document_id`.`name`,'')) as char charset utf8mb4)) AS `document_id_friendlyname`,`Document_document_id`.`finalclass` AS `document_id_finalclass_recall`,coalesce((`Document_document_id`.`status` = 'obsolete'),0) AS `document_id_obsolescence_flag` from ((`lnkdocumenttoservice` `lnkDocumentToService` join `service` `Service_service_id` on((`lnkDocumentToService`.`service_id` = `Service_service_id`.`id`))) join `document` `Document_document_id` on((`lnkDocumentToService`.`document_id` = `Document_document_id`.`id`))) where (0 <> 1)
```

