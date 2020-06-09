| 列                        | 类型                              | 注释 |
| :------------------------ | --------------------------------- | ---- |
| id                        | int [**0**]                       |      |
| name                      | varchar(255) *NULL* []            |      |
| org_id                    | int *NULL* [**0**]                |      |
| organization_name         | varchar(255) *NULL* []            |      |
| usage_limit               | varchar(255) *NULL* []            |      |
| description               | text *NULL*                       |      |
| start_date                | date *NULL*                       |      |
| end_date                  | date *NULL*                       |      |
| licence_key               | varchar(255) *NULL* []            |      |
| perpetual                 | enum('no','yes') *NULL* [**no**]  |      |
| osversion_id              | int *NULL* [**0**]                |      |
| osversion_name            | varchar(255) *NULL* []            |      |
| finalclass                | varchar(255) *NULL* [**Licence**] |      |
| friendlyname              | varchar(255) *NULL*               |      |
| obsolescence_flag         | int [**0**]                       |      |
| obsolescence_date         | date *NULL*                       |      |
| org_id_friendlyname       | varchar(255) *NULL*               |      |
| org_id_obsolescence_flag  | int [**0**]                       |      |
| osversion_id_friendlyname | varchar(255) *NULL*               |      |

```
select distinct `OSLicence`.`id` AS `id`,`OSLicence_Licence`.`name` AS `name`,`OSLicence_Licence`.`org_id` AS `org_id`,`Organization_org_id`.`name` AS `organization_name`,`OSLicence_Licence`.`usage_limit` AS `usage_limit`,`OSLicence_Licence`.`description` AS `description`,`OSLicence_Licence`.`start_date` AS `start_date`,`OSLicence_Licence`.`end_date` AS `end_date`,`OSLicence_Licence`.`licence_key` AS `licence_key`,`OSLicence_Licence`.`perpetual` AS `perpetual`,`OSLicence`.`osversion_id` AS `osversion_id`,`OSVersion_osversion_id_Typology`.`name` AS `osversion_name`,`OSLicence_Licence`.`finalclass` AS `finalclass`,cast(concat(coalesce(`OSLicence_Licence`.`name`,'')) as char charset utf8mb4) AS `friendlyname`,coalesce(((`OSLicence_Licence`.`perpetual` = 'no') and ((`OSLicence_Licence`.`end_date` is null) = 0) and (`OSLicence_Licence`.`end_date` < date_format((now() - interval 15 month),'%Y-%m-%d 00:00:00'))),0) AS `obsolescence_flag`,`OSLicence_Licence`.`obsolescence_date` AS `obsolescence_date`,cast(concat(coalesce(`Organization_org_id`.`name`,'')) as char charset utf8mb4) AS `org_id_friendlyname`,coalesce((`Organization_org_id`.`status` = 'inactive'),0) AS `org_id_obsolescence_flag`,cast(concat(coalesce(`OSVersion_osversion_id_Typology`.`name`,'')) as char charset utf8mb4) AS `osversion_id_friendlyname` from ((`oslicence` `OSLicence` join `typology` `OSVersion_osversion_id_Typology` on((`OSLicence`.`osversion_id` = `OSVersion_osversion_id_Typology`.`id`))) join (`licence` `OSLicence_Licence` join `organization` `Organization_org_id` on((`OSLicence_Licence`.`org_id` = `Organization_org_id`.`id`))) on((`OSLicence`.`id` = `OSLicence_Licence`.`id`))) where (0 <> coalesce((`OSVersion_osversion_id_Typology`.`finalclass` = 'OSVersion'),1))
```

