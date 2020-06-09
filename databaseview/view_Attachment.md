|                              |                                |      |
| :--------------------------- | ------------------------------ | ---- |
| 列                           | 类型                           | 注释 |
| id                           | int [**0**]                    |      |
| expire                       | datetime *NULL*                |      |
| temp_id                      | varchar(255) *NULL* []         |      |
| item_class                   | varchar(255) *NULL* []         |      |
| item_id                      | int *NULL* [**0**]             |      |
| item_org_id                  | int *NULL* [**0**]             |      |
| contents                     | varchar(255) *NULL*            |      |
| creation_date                | datetime *NULL*                |      |
| user_id                      | int *NULL* [**0**]             |      |
| contact_id                   | int *NULL* [**0**]             |      |
| friendlyname                 | varchar(511) *NULL*            |      |
| user_id_friendlyname         | varchar(255) *NULL*            |      |
| user_id_finalclass_recall    | varchar(255) *NULL* [**User**] |      |
| contact_id_friendlyname      | varchar(511) *NULL*            |      |
| contact_id_obsolescence_flag | int [**0**]                    |      |
| Attachmentcontents_data      | longblob *NULL*                |      |
| Attachmentcontents_filename  | varchar(255) *NULL*            |      |

```
select distinct `Attachment`.`id` AS `id`,`Attachment`.`expire` AS `expire`,`Attachment`.`temp_id` AS `temp_id`,`Attachment`.`item_class` AS `item_class`,`Attachment`.`item_id` AS `item_id`,`Attachment`.`item_org_id` AS `item_org_id`,`Attachment`.`contents_mimetype` AS `contents`,`Attachment`.`creation_date` AS `creation_date`,`Attachment`.`user_id` AS `user_id`,`User_user_id`.`contactid` AS `contact_id`,cast(concat(coalesce(`Attachment`.`item_class`,''),coalesce(' ',''),coalesce(`Attachment`.`temp_id`,'')) as char charset utf8mb4) AS `friendlyname`,cast(concat(coalesce(`User_user_id`.`login`,'')) as char charset utf8mb4) AS `user_id_friendlyname`,`User_user_id`.`finalclass` AS `user_id_finalclass_recall`,cast(concat(coalesce(`Person_contactid`.`first_name`,''),coalesce(' ',''),coalesce(`Person_contactid_Contact`.`name`,'')) as char charset utf8mb4) AS `contact_id_friendlyname`,coalesce((`Person_contactid_Contact`.`status` = 'inactive'),0) AS `contact_id_obsolescence_flag`,`Attachment`.`contents_data` AS `Attachmentcontents_data`,`Attachment`.`contents_filename` AS `Attachmentcontents_filename` from (`attachment` `Attachment` left join (`priv_user` `User_user_id` left join (`person` `Person_contactid` join `contact` `Person_contactid_Contact` on((`Person_contactid`.`id` = `Person_contactid_Contact`.`id`))) on((`User_user_id`.`contactid` = `Person_contactid`.`id`))) on((`Attachment`.`user_id` = `User_user_id`.`id`))) where (0 <> 1)
```

