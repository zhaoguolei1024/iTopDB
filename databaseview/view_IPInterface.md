| 列                | 类型                                       | 注释 |
| :---------------- | ------------------------------------------ | ---- |
| id                | int [**0**]                                |      |
| name              | varchar(255) *NULL* []                     |      |
| ipaddress         | varchar(255) *NULL* []                     |      |
| macaddress        | varchar(255) *NULL* []                     |      |
| comment           | text *NULL*                                |      |
| ipgateway         | varchar(255) *NULL* []                     |      |
| ipmask            | varchar(255) *NULL* []                     |      |
| speed             | decimal(12,2) *NULL*                       |      |
| finalclass        | varchar(255) *NULL* [**NetworkInterface**] |      |
| friendlyname      | varchar(511) *NULL*                        |      |
| obsolescence_flag | int [**0**]                                |      |
| obsolescence_date | date *NULL*                                |      |

```
SELECT DISTINCT
	`IPInterface`.`id` AS `id`,
	`IPInterface_NetworkInterface`.`name` AS `name`,
	`IPInterface`.`ipaddress` AS `ipaddress`,
	`IPInterface`.`macaddress` AS `macaddress`,
	`IPInterface`.`comment` AS `comment`,
	`IPInterface`.`ipgateway` AS `ipgateway`,
	`IPInterface`.`ipmask` AS `ipmask`,
	`IPInterface`.`speed` AS `speed`,
	`IPInterface_NetworkInterface`.`finalclass` AS `finalclass`,
IF
	((
			`IPInterface_NetworkInterface`.`finalclass` = 'IPInterface' 
			),
		cast( concat( COALESCE ( `IPInterface_NetworkInterface`.`name`, '' )) AS CHAR charset utf8mb4 ),
	IF
		((
				`IPInterface_NetworkInterface`.`finalclass` = 'LogicalInterface' 
				),
			cast(
				concat(
					COALESCE ( `IPInterface_NetworkInterface`.`name`, '' ),
					COALESCE ( ' ', '' ),
				COALESCE ( `VirtualMachine_virtualmachine_id_FunctionalCI`.`name`, '' )) AS CHAR charset utf8mb4 
			),
			cast(
				concat(
					COALESCE ( `IPInterface_NetworkInterface`.`name`, '' ),
					COALESCE ( ' ', '' ),
				COALESCE ( `ConnectableCI_connectableci_id_FunctionalCI`.`name`, '' )) AS CHAR charset utf8mb4 
			))) AS `friendlyname`,
IF
	((
			`IPInterface_NetworkInterface`.`finalclass` = 'IPInterface' 
			),
		COALESCE ( 0, 0 ),
	IF
		((
				`IPInterface_NetworkInterface`.`finalclass` = 'LogicalInterface' 
				),
			COALESCE ( COALESCE (( `VirtualMachine_virtualmachine_id_VirtualDevice`.`status` = 'obsolete' ), 0 ), 0 ),
		COALESCE ( COALESCE (( `ConnectableCI_connectableci_id_PhysicalDevice`.`status` = 'obsolete' ), 0 ), 0 ))) AS `obsolescence_flag`,
	`IPInterface_NetworkInterface`.`obsolescence_date` AS `obsolescence_date` 
FROM
	(((
				`ipinterface` `IPInterface`
				JOIN `networkinterface` `IPInterface_NetworkInterface` ON ((
						`IPInterface`.`id` = `IPInterface_NetworkInterface`.`id` 
					)))
			LEFT JOIN (
				`logicalinterface` `IPInterface_poly_LogicalInterface`
				JOIN (
					`virtualdevice` `VirtualMachine_virtualmachine_id_VirtualDevice`
					JOIN `functionalci` `VirtualMachine_virtualmachine_id_FunctionalCI` ON ((
							`VirtualMachine_virtualmachine_id_VirtualDevice`.`id` = `VirtualMachine_virtualmachine_id_FunctionalCI`.`id` 
							))) ON ((
						`IPInterface_poly_LogicalInterface`.`virtualmachine_id` = `VirtualMachine_virtualmachine_id_VirtualDevice`.`id` 
					))) ON ((
					`IPInterface`.`id` = `IPInterface_poly_LogicalInterface`.`id` 
				)))
		LEFT JOIN (
			`physicalinterface` `IPInterface_poly_PhysicalInterface`
			JOIN (
				`physicaldevice` `ConnectableCI_connectableci_id_PhysicalDevice`
				JOIN `functionalci` `ConnectableCI_connectableci_id_FunctionalCI` ON ((
						`ConnectableCI_connectableci_id_PhysicalDevice`.`id` = `ConnectableCI_connectableci_id_FunctionalCI`.`id` 
						))) ON ((
					`IPInterface_poly_PhysicalInterface`.`connectableci_id` = `ConnectableCI_connectableci_id_PhysicalDevice`.`id` 
				))) ON ((
				`IPInterface`.`id` = `IPInterface_poly_PhysicalInterface`.`id` 
			))) 
WHERE
	((
			0 <> COALESCE (( `VirtualMachine_virtualmachine_id_VirtualDevice`.`finalclass` = 'VirtualMachine' ), 1 )) 
	AND (
	0 <> COALESCE (( `ConnectableCI_connectableci_id_PhysicalDevice`.`finalclass` IN ( 'DatacenterDevice', 'NetworkDevice', 'Server', 'PC', 'Printer', 'StorageSystem', 'SANSwitch', 'TapeLibrary', 'NAS', 'ConnectableCI' )), 1 )))
```

