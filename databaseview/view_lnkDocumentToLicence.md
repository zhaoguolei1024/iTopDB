| 列                            | 类型                               | 注释 |
| :---------------------------- | ---------------------------------- | ---- |
| id                            | int [**0**]                        |      |
| licence_id                    | int *NULL* [**0**]                 |      |
| licence_name                  | varchar(255) *NULL* []             |      |
| document_id                   | int *NULL* [**0**]                 |      |
| document_name                 | varchar(255) *NULL* []             |      |
| friendlyname                  | varchar(23) *NULL*                 |      |
| licence_id_friendlyname       | varchar(255) *NULL*                |      |
| licence_id_finalclass_recall  | varchar(255) *NULL* [**Licence**]  |      |
| licence_id_obsolescence_flag  | int [**0**]                        |      |
| document_id_friendlyname      | varchar(255) *NULL*                |      |
| document_id_finalclass_recall | varchar(255) *NULL* [**Document**] |      |
| document_id_obsolescence_flag | int [**0**]                        |      |

```
select distinct `lnkDocumentToLicence`.`id` AS `id`,`lnkDocumentToLicence`.`licence_id` AS `licence_id`,`Licence_licence_id`.`name` AS `licence_name`,`lnkDocumentToLicence`.`document_id` AS `document_id`,`Document_document_id`.`name` AS `document_name`,cast(concat(coalesce(`lnkDocumentToLicence`.`licence_id`,''),coalesce(' ',''),coalesce(`lnkDocumentToLicence`.`document_id`,'')) as char charset utf8mb4) AS `friendlyname`,cast(concat(coalesce(`Licence_licence_id`.`name`,'')) as char charset utf8mb4) AS `licence_id_friendlyname`,`Licence_licence_id`.`finalclass` AS `licence_id_finalclass_recall`,coalesce(((`Licence_licence_id`.`perpetual` = 'no') and ((`Licence_licence_id`.`end_date` is null) = 0) and (`Licence_licence_id`.`end_date` < date_format((now() - interval 15 month),'%Y-%m-%d 00:00:00'))),0) AS `licence_id_obsolescence_flag`,if((`Document_document_id`.`finalclass` = 'Document'),cast(concat(coalesce('Document','')) as char charset utf8mb4),cast(concat(coalesce(`Document_document_id`.`name`,'')) as char charset utf8mb4)) AS `document_id_friendlyname`,`Document_document_id`.`finalclass` AS `document_id_finalclass_recall`,coalesce((`Document_document_id`.`status` = 'obsolete'),0) AS `document_id_obsolescence_flag` from ((`lnkdocumenttolicence` `lnkDocumentToLicence` join `licence` `Licence_licence_id` on((`lnkDocumentToLicence`.`licence_id` = `Licence_licence_id`.`id`))) join `document` `Document_document_id` on((`lnkDocumentToLicence`.`document_id` = `Document_document_id`.`id`))) where (0 <> 1)
```

