| 列                                 | 类型                                       | 注释 |
| :--------------------------------- | ------------------------------------------ | ---- |
| id                                 | int [**0**]                                |      |
| name                               | varchar(255) *NULL* []                     |      |
| ipaddress                          | varchar(255) *NULL* []                     |      |
| macaddress                         | varchar(255) *NULL* []                     |      |
| comment                            | text *NULL*                                |      |
| ipgateway                          | varchar(255) *NULL* []                     |      |
| ipmask                             | varchar(255) *NULL* []                     |      |
| speed                              | decimal(12,2) *NULL*                       |      |
| connectableci_id                   | int *NULL* [**0**]                         |      |
| connectableci_name                 | varchar(255) *NULL* []                     |      |
| finalclass                         | varchar(255) *NULL* [**NetworkInterface**] |      |
| friendlyname                       | varchar(511) *NULL*                        |      |
| obsolescence_flag                  | int [**0**]                                |      |
| obsolescence_date                  | date *NULL*                                |      |
| connectableci_id_friendlyname      | varchar(255) *NULL*                        |      |
| connectableci_id_finalclass_recall | varchar(255) *NULL* [**FunctionalCI**]     |      |
| connectableci_id_obsolescence_flag | int [**0**]                                |      |

```
SELECT DISTINCT
	`PhysicalInterface`.`id` AS `id`,
	`PhysicalInterface_NetworkInterface`.`name` AS `name`,
	`PhysicalInterface_IPInterface`.`ipaddress` AS `ipaddress`,
	`PhysicalInterface_IPInterface`.`macaddress` AS `macaddress`,
	`PhysicalInterface_IPInterface`.`comment` AS `comment`,
	`PhysicalInterface_IPInterface`.`ipgateway` AS `ipgateway`,
	`PhysicalInterface_IPInterface`.`ipmask` AS `ipmask`,
	`PhysicalInterface_IPInterface`.`speed` AS `speed`,
	`PhysicalInterface`.`connectableci_id` AS `connectableci_id`,
	`ConnectableCI_connectableci_id_FunctionalCI`.`name` AS `connectableci_name`,
	`PhysicalInterface_NetworkInterface`.`finalclass` AS `finalclass`,
	cast(
		concat(
			COALESCE ( `PhysicalInterface_NetworkInterface`.`name`, '' ),
			COALESCE ( ' ', '' ),
		COALESCE ( `ConnectableCI_connectableci_id_FunctionalCI`.`name`, '' )) AS CHAR charset utf8mb4 
	) AS `friendlyname`,
	COALESCE ( COALESCE (( `ConnectableCI_connectableci_id_PhysicalDevice`.`status` = 'obsolete' ), 0 ), 0 ) AS `obsolescence_flag`,
	`PhysicalInterface_NetworkInterface`.`obsolescence_date` AS `obsolescence_date`,
	cast( concat( COALESCE ( `ConnectableCI_connectableci_id_FunctionalCI`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `connectableci_id_friendlyname`,
	`ConnectableCI_connectableci_id_FunctionalCI`.`finalclass` AS `connectableci_id_finalclass_recall`,
	COALESCE (( `ConnectableCI_connectableci_id_PhysicalDevice`.`status` = 'obsolete' ), 0 ) AS `connectableci_id_obsolescence_flag` 
FROM
	(((
				`physicalinterface` `PhysicalInterface`
				JOIN (
					`physicaldevice` `ConnectableCI_connectableci_id_PhysicalDevice`
					JOIN `functionalci` `ConnectableCI_connectableci_id_FunctionalCI` ON ((
							`ConnectableCI_connectableci_id_PhysicalDevice`.`id` = `ConnectableCI_connectableci_id_FunctionalCI`.`id` 
							))) ON ((
						`PhysicalInterface`.`connectableci_id` = `ConnectableCI_connectableci_id_PhysicalDevice`.`id` 
					)))
			JOIN `ipinterface` `PhysicalInterface_IPInterface` ON ((
					`PhysicalInterface`.`id` = `PhysicalInterface_IPInterface`.`id` 
				)))
		JOIN `networkinterface` `PhysicalInterface_NetworkInterface` ON ((
				`PhysicalInterface`.`id` = `PhysicalInterface_NetworkInterface`.`id` 
			))) 
WHERE
	(
	0 <> COALESCE (( `ConnectableCI_connectableci_id_PhysicalDevice`.`finalclass` IN ( 'DatacenterDevice', 'NetworkDevice', 'Server', 'PC', 'Printer', 'StorageSystem', 'SANSwitch', 'TapeLibrary', 'NAS', 'ConnectableCI' )), 1 ))
```

