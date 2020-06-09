| 列                            | 类型                               | 注释 |
| :---------------------------- | ---------------------------------- | ---- |
| id                            | int [**0**]                        |      |
| patch_id                      | int *NULL* [**0**]                 |      |
| patch_name                    | varchar(255) *NULL* []             |      |
| document_id                   | int *NULL* [**0**]                 |      |
| document_name                 | varchar(255) *NULL* []             |      |
| friendlyname                  | varchar(23) *NULL*                 |      |
| patch_id_friendlyname         | varchar(255) *NULL*                |      |
| patch_id_finalclass_recall    | varchar(255) *NULL* [**Patch**]    |      |
| document_id_friendlyname      | varchar(255) *NULL*                |      |
| document_id_finalclass_recall | varchar(255) *NULL* [**Document**] |      |
| document_id_obsolescence_flag | int [**0**]                        |      |

```
select distinct `lnkDocumentToPatch`.`id` AS `id`,`lnkDocumentToPatch`.`patch_id` AS `patch_id`,`Patch_patch_id`.`name` AS `patch_name`,`lnkDocumentToPatch`.`document_id` AS `document_id`,`Document_document_id`.`name` AS `document_name`,cast(concat(coalesce(`lnkDocumentToPatch`.`patch_id`,''),coalesce(' ',''),coalesce(`lnkDocumentToPatch`.`document_id`,'')) as char charset utf8mb4) AS `friendlyname`,cast(concat(coalesce(`Patch_patch_id`.`name`,'')) as char charset utf8mb4) AS `patch_id_friendlyname`,`Patch_patch_id`.`finalclass` AS `patch_id_finalclass_recall`,if((`Document_document_id`.`finalclass` = 'Document'),cast(concat(coalesce('Document','')) as char charset utf8mb4),cast(concat(coalesce(`Document_document_id`.`name`,'')) as char charset utf8mb4)) AS `document_id_friendlyname`,`Document_document_id`.`finalclass` AS `document_id_finalclass_recall`,coalesce((`Document_document_id`.`status` = 'obsolete'),0) AS `document_id_obsolescence_flag` from ((`lnkdocumenttopatch` `lnkDocumentToPatch` join `patch` `Patch_patch_id` on((`lnkDocumentToPatch`.`patch_id` = `Patch_patch_id`.`id`))) join `document` `Document_document_id` on((`lnkDocumentToPatch`.`document_id` = `Document_document_id`.`id`))) where (0 <> 1)
```

