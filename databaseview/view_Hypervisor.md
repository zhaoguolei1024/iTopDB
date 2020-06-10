| 列                          | 类型                                                         | 注释 |
| :-------------------------- | ------------------------------------------------------------ | ---- |
| id                          | int [**0**]                                                  |      |
| name                        | varchar(255) *NULL* []                                       |      |
| description                 | text *NULL*                                                  |      |
| org_id                      | int *NULL* [**0**]                                           |      |
| organization_name           | varchar(255) *NULL* []                                       |      |
| business_criticity          | enum('high','low','medium') *NULL* [**low**]                 |      |
| move2production             | date *NULL*                                                  |      |
| status                      | enum('implementation','obsolete','production','stock') *NULL* [**production**] |      |
| farm_id                     | int *NULL* [**0**]                                           |      |
| farm_name                   | varchar(255) *NULL* []                                       |      |
| server_id                   | int *NULL* [**0**]                                           |      |
| server_name                 | varchar(255) *NULL* []                                       |      |
| finalclass                  | varchar(255) *NULL* [**FunctionalCI**]                       |      |
| friendlyname                | varchar(255) *NULL*                                          |      |
| obsolescence_flag           | int [**0**]                                                  |      |
| obsolescence_date           | date *NULL*                                                  |      |
| org_id_friendlyname         | varchar(255) *NULL*                                          |      |
| org_id_obsolescence_flag    | int [**0**]                                                  |      |
| farm_id_friendlyname        | varchar(255) *NULL*                                          |      |
| farm_id_obsolescence_flag   | int [**0**]                                                  |      |
| server_id_friendlyname      | varchar(255) *NULL*                                          |      |
| server_id_obsolescence_flag | int [**0**]                                                  |      |

```
SELECT DISTINCT
	`Hypervisor`.`id` AS `id`,
	`Hypervisor_FunctionalCI`.`name` AS `name`,
	`Hypervisor_FunctionalCI`.`description` AS `description`,
	`Hypervisor_FunctionalCI`.`org_id` AS `org_id`,
	`Organization_org_id`.`name` AS `organization_name`,
	`Hypervisor_FunctionalCI`.`business_criticity` AS `business_criticity`,
	`Hypervisor_FunctionalCI`.`move2production` AS `move2production`,
	`Hypervisor_VirtualDevice`.`status` AS `status`,
	`Hypervisor`.`farm_id` AS `farm_id`,
	`Farm_farm_id_FunctionalCI`.`name` AS `farm_name`,
	`Hypervisor`.`server_id` AS `server_id`,
	`Server_server_id_FunctionalCI`.`name` AS `server_name`,
	`Hypervisor_FunctionalCI`.`finalclass` AS `finalclass`,
	cast( concat( COALESCE ( `Hypervisor_FunctionalCI`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `friendlyname`,
	COALESCE (( `Hypervisor_VirtualDevice`.`status` = 'obsolete' ), 0 ) AS `obsolescence_flag`,
	`Hypervisor_FunctionalCI`.`obsolescence_date` AS `obsolescence_date`,
	cast( concat( COALESCE ( `Organization_org_id`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `org_id_friendlyname`,
	COALESCE (( `Organization_org_id`.`status` = 'inactive' ), 0 ) AS `org_id_obsolescence_flag`,
	cast( concat( COALESCE ( `Farm_farm_id_FunctionalCI`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `farm_id_friendlyname`,
	COALESCE (( `Farm_farm_id_VirtualDevice`.`status` = 'obsolete' ), 0 ) AS `farm_id_obsolescence_flag`,
	cast( concat( COALESCE ( `Server_server_id_FunctionalCI`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `server_id_friendlyname`,
	COALESCE (( `Server_server_id_PhysicalDevice`.`status` = 'obsolete' ), 0 ) AS `server_id_obsolescence_flag` 
FROM
	((((
					`hypervisor` `Hypervisor`
					LEFT JOIN (
						`virtualdevice` `Farm_farm_id_VirtualDevice`
						JOIN `functionalci` `Farm_farm_id_FunctionalCI` ON ((
								`Farm_farm_id_VirtualDevice`.`id` = `Farm_farm_id_FunctionalCI`.`id` 
								))) ON ((
							`Hypervisor`.`farm_id` = `Farm_farm_id_VirtualDevice`.`id` 
						)))
				LEFT JOIN (
					`physicaldevice` `Server_server_id_PhysicalDevice`
					JOIN `functionalci` `Server_server_id_FunctionalCI` ON ((
							`Server_server_id_PhysicalDevice`.`id` = `Server_server_id_FunctionalCI`.`id` 
							))) ON ((
						`Hypervisor`.`server_id` = `Server_server_id_PhysicalDevice`.`id` 
					)))
			JOIN `virtualdevice` `Hypervisor_VirtualDevice` ON ((
					`Hypervisor`.`id` = `Hypervisor_VirtualDevice`.`id` 
				)))
		JOIN (
			`functionalci` `Hypervisor_FunctionalCI`
			JOIN `organization` `Organization_org_id` ON ((
					`Hypervisor_FunctionalCI`.`org_id` = `Organization_org_id`.`id` 
					))) ON ((
				`Hypervisor`.`id` = `Hypervisor_FunctionalCI`.`id` 
			))) 
WHERE
	((
			0 <> COALESCE (( `Farm_farm_id_VirtualDevice`.`finalclass` = 'Farm' ), 1 )) 
	AND (
	0 <> COALESCE (( `Server_server_id_PhysicalDevice`.`finalclass` = 'Server' ), 1 )))
```

