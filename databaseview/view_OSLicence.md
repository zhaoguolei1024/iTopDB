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
SELECT DISTINCT
	`OSLicence`.`id` AS `id`,
	`OSLicence_Licence`.`name` AS `name`,
	`OSLicence_Licence`.`org_id` AS `org_id`,
	`Organization_org_id`.`name` AS `organization_name`,
	`OSLicence_Licence`.`usage_limit` AS `usage_limit`,
	`OSLicence_Licence`.`description` AS `description`,
	`OSLicence_Licence`.`start_date` AS `start_date`,
	`OSLicence_Licence`.`end_date` AS `end_date`,
	`OSLicence_Licence`.`licence_key` AS `licence_key`,
	`OSLicence_Licence`.`perpetual` AS `perpetual`,
	`OSLicence`.`osversion_id` AS `osversion_id`,
	`OSVersion_osversion_id_Typology`.`name` AS `osversion_name`,
	`OSLicence_Licence`.`finalclass` AS `finalclass`,
	cast( concat( COALESCE ( `OSLicence_Licence`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `friendlyname`,
	COALESCE (((
				`OSLicence_Licence`.`perpetual` = 'no' 
				) 
			AND (( `OSLicence_Licence`.`end_date` IS NULL ) = 0 ) 
			AND (
			`OSLicence_Licence`.`end_date` < date_format(( now() - INTERVAL 15 MONTH ), '%Y-%m-%d 00:00:00' ))),
		0 
	) AS `obsolescence_flag`,
	`OSLicence_Licence`.`obsolescence_date` AS `obsolescence_date`,
	cast( concat( COALESCE ( `Organization_org_id`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `org_id_friendlyname`,
	COALESCE (( `Organization_org_id`.`status` = 'inactive' ), 0 ) AS `org_id_obsolescence_flag`,
	cast( concat( COALESCE ( `OSVersion_osversion_id_Typology`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `osversion_id_friendlyname` 
FROM
	((
			`oslicence` `OSLicence`
			JOIN `typology` `OSVersion_osversion_id_Typology` ON ((
					`OSLicence`.`osversion_id` = `OSVersion_osversion_id_Typology`.`id` 
				)))
		JOIN (
			`licence` `OSLicence_Licence`
			JOIN `organization` `Organization_org_id` ON ((
					`OSLicence_Licence`.`org_id` = `Organization_org_id`.`id` 
					))) ON ((
				`OSLicence`.`id` = `OSLicence_Licence`.`id` 
			))) 
WHERE
	(
	0 <> COALESCE (( `OSVersion_osversion_id_Typology`.`finalclass` = 'OSVersion' ), 1 ))
```

