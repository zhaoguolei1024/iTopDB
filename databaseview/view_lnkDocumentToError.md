| 列                            | 类型                               | 注释 |
| :---------------------------- | ---------------------------------- | ---- |
| id                            | int [**0**]                        |      |
| document_id                   | int *NULL* [**0**]                 |      |
| document_name                 | varchar(255) *NULL* []             |      |
| error_id                      | int *NULL* [**0**]                 |      |
| error_name                    | varchar(255) *NULL* []             |      |
| link_type                     | varchar(255) *NULL* []             |      |
| friendlyname                  | varchar(255) *NULL*                |      |
| document_id_friendlyname      | varchar(255) *NULL*                |      |
| document_id_finalclass_recall | varchar(255) *NULL* [**Document**] |      |
| document_id_obsolescence_flag | int [**0**]                        |      |
| error_id_friendlyname         | varchar(255) *NULL*                |      |

```
select distinct `lnkDocumentToError`.`link_id` AS `id`,`lnkDocumentToError`.`document_id` AS `document_id`,`Document_document_id`.`name` AS `document_name`,`lnkDocumentToError`.`error_id` AS `error_id`,`KnownError_error_id`.`name` AS `error_name`,`lnkDocumentToError`.`link_type` AS `link_type`,cast(concat(coalesce(`lnkDocumentToError`.`link_type`,'')) as char charset utf8mb4) AS `friendlyname`,if((`Document_document_id`.`finalclass` = 'Document'),cast(concat(coalesce('Document','')) as char charset utf8mb4),cast(concat(coalesce(`Document_document_id`.`name`,'')) as char charset utf8mb4)) AS `document_id_friendlyname`,`Document_document_id`.`finalclass` AS `document_id_finalclass_recall`,coalesce((`Document_document_id`.`status` = 'obsolete'),0) AS `document_id_obsolescence_flag`,cast(concat(coalesce(`KnownError_error_id`.`name`,'')) as char charset utf8mb4) AS `error_id_friendlyname` from ((`lnkdocumenttoerror` `lnkDocumentToError` join `document` `Document_document_id` on((`lnkDocumentToError`.`document_id` = `Document_document_id`.`id`))) join `knownerror` `KnownError_error_id` on((`lnkDocumentToError`.`error_id` = `KnownError_error_id`.`id`))) where (0 <> 1)
```

