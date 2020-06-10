| 列                               | 类型                                                         | 注释 |
| :------------------------------- | ------------------------------------------------------------ | ---- |
| id                               | int [**0**]                                                  |      |
| name                             | varchar(255) *NULL* []                                       |      |
| description                      | text *NULL*                                                  |      |
| org_id                           | int *NULL* [**0**]                                           |      |
| organization_name                | varchar(255) *NULL* []                                       |      |
| business_criticity               | enum('high','low','medium') *NULL* [**low**]                 |      |
| move2production                  | date *NULL*                                                  |      |
| status                           | enum('implementation','obsolete','production','stock') *NULL* [**production**] |      |
| virtualhost_id                   | int *NULL* [**0**]                                           |      |
| virtualhost_name                 | varchar(255) *NULL* []                                       |      |
| osfamily_id                      | int *NULL* [**0**]                                           |      |
| osfamily_name                    | varchar(255) *NULL* []                                       |      |
| osversion_id                     | int *NULL* [**0**]                                           |      |
| osversion_name                   | varchar(255) *NULL* []                                       |      |
| oslicence_id                     | int *NULL* [**0**]                                           |      |
| oslicence_name                   | varchar(255) *NULL* []                                       |      |
| cpu                              | varchar(255) *NULL* []                                       |      |
| ram                              | varchar(255) *NULL* []                                       |      |
| managementip                     | varchar(255) *NULL* []                                       |      |
| finalclass                       | varchar(255) *NULL* [**FunctionalCI**]                       |      |
| friendlyname                     | varchar(255) *NULL*                                          |      |
| obsolescence_flag                | int [**0**]                                                  |      |
| obsolescence_date                | date *NULL*                                                  |      |
| org_id_friendlyname              | varchar(255) *NULL*                                          |      |
| org_id_obsolescence_flag         | int [**0**]                                                  |      |
| virtualhost_id_friendlyname      | varchar(255) *NULL*                                          |      |
| virtualhost_id_finalclass_recall | varchar(255) *NULL* [**FunctionalCI**]                       |      |
| virtualhost_id_obsolescence_flag | int [**0**]                                                  |      |
| osfamily_id_friendlyname         | varchar(255) *NULL*                                          |      |
| osversion_id_friendlyname        | varchar(255) *NULL*                                          |      |
| oslicence_id_friendlyname        | varchar(255) *NULL*                                          |      |
| oslicence_id_obsolescence_flag   | int [**0**]                                                  |      |

```
SELECT DISTINCT
	`VirtualMachine`.`id` AS `id`,
	`VirtualMachine_FunctionalCI`.`name` AS `name`,
	`VirtualMachine_FunctionalCI`.`description` AS `description`,
	`VirtualMachine_FunctionalCI`.`org_id` AS `org_id`,
	`Organization_org_id`.`name` AS `organization_name`,
	`VirtualMachine_FunctionalCI`.`business_criticity` AS `business_criticity`,
	`VirtualMachine_FunctionalCI`.`move2production` AS `move2production`,
	`VirtualMachine_VirtualDevice`.`status` AS `status`,
	`VirtualMachine`.`virtualhost_id` AS `virtualhost_id`,
	`VirtualHost_virtualhost_id_FunctionalCI`.`name` AS `virtualhost_name`,
	`VirtualMachine`.`osfamily_id` AS `osfamily_id`,
	`OSFamily_osfamily_id_Typology`.`name` AS `osfamily_name`,
	`VirtualMachine`.`osversion_id` AS `osversion_id`,
	`OSVersion_osversion_id_Typology`.`name` AS `osversion_name`,
	`VirtualMachine`.`oslicence_id` AS `oslicence_id`,
	`OSLicence_oslicence_id_Licence`.`name` AS `oslicence_name`,
	`VirtualMachine`.`cpu` AS `cpu`,
	`VirtualMachine`.`ram` AS `ram`,
	`VirtualMachine`.`managementip` AS `managementip`,
	`VirtualMachine_FunctionalCI`.`finalclass` AS `finalclass`,
	cast( concat( COALESCE ( `VirtualMachine_FunctionalCI`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `friendlyname`,
	COALESCE (( `VirtualMachine_VirtualDevice`.`status` = 'obsolete' ), 0 ) AS `obsolescence_flag`,
	`VirtualMachine_FunctionalCI`.`obsolescence_date` AS `obsolescence_date`,
	cast( concat( COALESCE ( `Organization_org_id`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `org_id_friendlyname`,
	COALESCE (( `Organization_org_id`.`status` = 'inactive' ), 0 ) AS `org_id_obsolescence_flag`,
	cast( concat( COALESCE ( `VirtualHost_virtualhost_id_FunctionalCI`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `virtualhost_id_friendlyname`,
	`VirtualHost_virtualhost_id_FunctionalCI`.`finalclass` AS `virtualhost_id_finalclass_recall`,
	COALESCE (( `VirtualHost_virtualhost_id_VirtualDevice`.`status` = 'obsolete' ), 0 ) AS `virtualhost_id_obsolescence_flag`,
	cast( concat( COALESCE ( `OSFamily_osfamily_id_Typology`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `osfamily_id_friendlyname`,
	cast( concat( COALESCE ( `OSVersion_osversion_id_Typology`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `osversion_id_friendlyname`,
	cast( concat( COALESCE ( `OSLicence_oslicence_id_Licence`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `oslicence_id_friendlyname`,
	COALESCE (((
				`OSLicence_oslicence_id_Licence`.`perpetual` = 'no' 
				) 
			AND (( `OSLicence_oslicence_id_Licence`.`end_date` IS NULL ) = 0 ) 
			AND (
			`OSLicence_oslicence_id_Licence`.`end_date` < date_format(( now() - INTERVAL 15 MONTH ), '%Y-%m-%d 00:00:00' ))),
		0 
	) AS `oslicence_id_obsolescence_flag` 
FROM
	((((((
							`virtualmachine` `VirtualMachine`
							JOIN (
								`virtualdevice` `VirtualHost_virtualhost_id_VirtualDevice`
								JOIN `functionalci` `VirtualHost_virtualhost_id_FunctionalCI` ON ((
										`VirtualHost_virtualhost_id_VirtualDevice`.`id` = `VirtualHost_virtualhost_id_FunctionalCI`.`id` 
										))) ON ((
									`VirtualMachine`.`virtualhost_id` = `VirtualHost_virtualhost_id_VirtualDevice`.`id` 
								)))
						LEFT JOIN `typology` `OSFamily_osfamily_id_Typology` ON ((
								`VirtualMachine`.`osfamily_id` = `OSFamily_osfamily_id_Typology`.`id` 
							)))
					LEFT JOIN `typology` `OSVersion_osversion_id_Typology` ON ((
							`VirtualMachine`.`osversion_id` = `OSVersion_osversion_id_Typology`.`id` 
						)))
				LEFT JOIN `licence` `OSLicence_oslicence_id_Licence` ON ((
						`VirtualMachine`.`oslicence_id` = `OSLicence_oslicence_id_Licence`.`id` 
					)))
			JOIN `virtualdevice` `VirtualMachine_VirtualDevice` ON ((
					`VirtualMachine`.`id` = `VirtualMachine_VirtualDevice`.`id` 
				)))
		JOIN (
			`functionalci` `VirtualMachine_FunctionalCI`
			JOIN `organization` `Organization_org_id` ON ((
					`VirtualMachine_FunctionalCI`.`org_id` = `Organization_org_id`.`id` 
					))) ON ((
				`VirtualMachine`.`id` = `VirtualMachine_FunctionalCI`.`id` 
			))) 
WHERE
	((
			0 <> COALESCE (( `VirtualHost_virtualhost_id_VirtualDevice`.`finalclass` IN ( 'Hypervisor', 'Farm', 'VirtualHost' )), 1 )) 
		AND (
		0 <> COALESCE (( `OSFamily_osfamily_id_Typology`.`finalclass` = 'OSFamily' ), 1 )) 
		AND (
		0 <> COALESCE (( `OSVersion_osversion_id_Typology`.`finalclass` = 'OSVersion' ), 1 )) 
	AND (
	0 <> COALESCE (( `OSLicence_oslicence_id_Licence`.`finalclass` = 'OSLicence' ), 1 )))
```

