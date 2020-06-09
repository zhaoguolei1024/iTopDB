| 列                           | 类型                                        | 注释 |
| :--------------------------- | ------------------------------------------- | ---- |
| id                           | int [**0**]                                 |      |
| name                         | varchar(255) *NULL* []                      |      |
| org_id                       | int *NULL* [**0**]                          |      |
| org_name                     | varchar(255) *NULL* []                      |      |
| documenttype_id              | int *NULL* [**0**]                          |      |
| documenttype_name            | varchar(255) *NULL* []                      |      |
| version                      | varchar(255) *NULL* []                      |      |
| description                  | text *NULL*                                 |      |
| status                       | enum('draft','obsolete','published') *NULL* |      |
| finalclass                   | varchar(255) *NULL* [**Document**]          |      |
| friendlyname                 | varchar(255) *NULL*                         |      |
| obsolescence_flag            | int [**0**]                                 |      |
| obsolescence_date            | date *NULL*                                 |      |
| org_id_friendlyname          | varchar(255) *NULL*                         |      |
| org_id_obsolescence_flag     | int [**0**]                                 |      |
| documenttype_id_friendlyname | varchar(255) *NULL*                         |      |

```
select distinct `Document`.`id` AS `id`,`Document`.`name` AS `name`,`Document`.`org_id` AS `org_id`,`Organization_org_id`.`name` AS `org_name`,`Document`.`documenttype_id` AS `documenttype_id`,`DocumentType_documenttype_id_Typology`.`name` AS `documenttype_name`,`Document`.`version` AS `version`,`Document`.`description` AS `description`,`Document`.`status` AS `status`,`Document`.`finalclass` AS `finalclass`,if((`Document`.`finalclass` = 'Document'),cast(concat(coalesce('Document','')) as char charset utf8mb4),cast(concat(coalesce(`Document`.`name`,'')) as char charset utf8mb4)) AS `friendlyname`,coalesce((`Document`.`status` = 'obsolete'),0) AS `obsolescence_flag`,`Document`.`obsolescence_date` AS `obsolescence_date`,cast(concat(coalesce(`Organization_org_id`.`name`,'')) as char charset utf8mb4) AS `org_id_friendlyname`,coalesce((`Organization_org_id`.`status` = 'inactive'),0) AS `org_id_obsolescence_flag`,cast(concat(coalesce(`DocumentType_documenttype_id_Typology`.`name`,'')) as char charset utf8mb4) AS `documenttype_id_friendlyname` from ((`document` `Document` join `organization` `Organization_org_id` on((`Document`.`org_id` = `Organization_org_id`.`id`))) left join `typology` `DocumentType_documenttype_id_Typology` on((`Document`.`documenttype_id` = `DocumentType_documenttype_id_Typology`.`id`))) where (0 <> coalesce((`DocumentType_documenttype_id_Typology`.`finalclass` = 'DocumentType'),1))
```

