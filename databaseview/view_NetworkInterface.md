| 列                | 类型                                       | 注释 |
| :---------------- | ------------------------------------------ | ---- |
| id                | int [**0**]                                |      |
| name              | varchar(255) *NULL* []                     |      |
| finalclass        | varchar(255) *NULL* [**NetworkInterface**] |      |
| friendlyname      | varchar(511) *NULL*                        |      |
| obsolescence_flag | int [**0**]                                |      |
| obsolescence_date | date *NULL*                                |      |

```
SELECT DISTINCT
	`NetworkInterface`.`id` AS `id`,
	`NetworkInterface`.`name` AS `name`,
	`NetworkInterface`.`finalclass` AS `finalclass`,
IF
	((
			`NetworkInterface`.`finalclass` = 'NetworkInterface' 
			),
		cast( concat( COALESCE ( `NetworkInterface`.`name`, '' )) AS CHAR charset utf8mb4 ),
	IF
		((
				`NetworkInterface`.`finalclass` = 'LogicalInterface' 
				),
			cast(
				concat(
					COALESCE ( `NetworkInterface`.`name`, '' ),
					COALESCE ( ' ', '' ),
				COALESCE ( `VirtualMachine_virtualmachine_id_FunctionalCI`.`name`, '' )) AS CHAR charset utf8mb4 
			),
		IF
			((
					`NetworkInterface`.`finalclass` = 'FiberChannelInterface' 
					),
				cast(
					concat(
						COALESCE ( `NetworkInterface`.`name`, '' ),
						COALESCE ( ' ', '' ),
					COALESCE ( `DatacenterDevice_datacenterdevice_id_FunctionalCI`.`name`, '' )) AS CHAR charset utf8mb4 
				),
				cast(
					concat(
						COALESCE ( `NetworkInterface`.`name`, '' ),
						COALESCE ( ' ', '' ),
					COALESCE ( `ConnectableCI_connectableci_id_FunctionalCI`.`name`, '' )) AS CHAR charset utf8mb4 
				)))) AS `friendlyname`,
IF
	((
			`NetworkInterface`.`finalclass` = 'NetworkInterface' 
			),
		COALESCE ( 0, 0 ),
	IF
		((
				`NetworkInterface`.`finalclass` = 'LogicalInterface' 
				),
			COALESCE ( COALESCE (( `VirtualMachine_virtualmachine_id_VirtualDevice`.`status` = 'obsolete' ), 0 ), 0 ),
		IF
			((
					`NetworkInterface`.`finalclass` = 'FiberChannelInterface' 
					),
				COALESCE ( COALESCE (( `DatacenterDevice_datacenterdevice_id_PhysicalDevice`.`status` = 'obsolete' ), 0 ), 0 ),
			COALESCE ( COALESCE (( `ConnectableCI_connectableci_id_PhysicalDevice`.`status` = 'obsolete' ), 0 ), 0 )))) AS `obsolescence_flag`,
	`NetworkInterface`.`obsolescence_date` AS `obsolescence_date` 
FROM
	(((
				`networkinterface` `NetworkInterface`
				LEFT JOIN (
					`logicalinterface` `NetworkInterface_poly_LogicalInterface`
					JOIN (
						`virtualdevice` `VirtualMachine_virtualmachine_id_VirtualDevice`
						JOIN `functionalci` `VirtualMachine_virtualmachine_id_FunctionalCI` ON ((
								`VirtualMachine_virtualmachine_id_VirtualDevice`.`id` = `VirtualMachine_virtualmachine_id_FunctionalCI`.`id` 
								))) ON ((
							`NetworkInterface_poly_LogicalInterface`.`virtualmachine_id` = `VirtualMachine_virtualmachine_id_VirtualDevice`.`id` 
						))) ON ((
						`NetworkInterface`.`id` = `NetworkInterface_poly_LogicalInterface`.`id` 
					)))
			LEFT JOIN (
				`fiberchannelinterface` `NetworkInterface_poly_FiberChannelInterface`
				JOIN (
					`physicaldevice` `DatacenterDevice_datacenterdevice_id_PhysicalDevice`
					JOIN `functionalci` `DatacenterDevice_datacenterdevice_id_FunctionalCI` ON ((
							`DatacenterDevice_datacenterdevice_id_PhysicalDevice`.`id` = `DatacenterDevice_datacenterdevice_id_FunctionalCI`.`id` 
							))) ON ((
						`NetworkInterface_poly_FiberChannelInterface`.`datacenterdevice_id` = `DatacenterDevice_datacenterdevice_id_PhysicalDevice`.`id` 
					))) ON ((
					`NetworkInterface`.`id` = `NetworkInterface_poly_FiberChannelInterface`.`id` 
				)))
		LEFT JOIN (
			`physicalinterface` `NetworkInterface_poly_PhysicalInterface`
			JOIN (
				`physicaldevice` `ConnectableCI_connectableci_id_PhysicalDevice`
				JOIN `functionalci` `ConnectableCI_connectableci_id_FunctionalCI` ON ((
						`ConnectableCI_connectableci_id_PhysicalDevice`.`id` = `ConnectableCI_connectableci_id_FunctionalCI`.`id` 
						))) ON ((
					`NetworkInterface_poly_PhysicalInterface`.`connectableci_id` = `ConnectableCI_connectableci_id_PhysicalDevice`.`id` 
				))) ON ((
				`NetworkInterface`.`id` = `NetworkInterface_poly_PhysicalInterface`.`id` 
			))) 
WHERE
	((
			0 <> COALESCE (( `VirtualMachine_virtualmachine_id_VirtualDevice`.`finalclass` = 'VirtualMachine' ), 1 )) 
		AND (
		0 <> COALESCE (( `DatacenterDevice_datacenterdevice_id_PhysicalDevice`.`finalclass` IN ( 'NetworkDevice', 'Server', 'StorageSystem', 'SANSwitch', 'TapeLibrary', 'NAS', 'DatacenterDevice' )), 1 )) 
	AND (
	0 <> COALESCE (( `ConnectableCI_connectableci_id_PhysicalDevice`.`finalclass` IN ( 'DatacenterDevice', 'NetworkDevice', 'Server', 'PC', 'Printer', 'StorageSystem', 'SANSwitch', 'TapeLibrary', 'NAS', 'ConnectableCI' )), 1 )))
```

