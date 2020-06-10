| 列                                            | 类型                   | 注释 |
| :-------------------------------------------- | ---------------------- | ---- |
| id                                            | int [**0**]            |      |
| physicalinterface_id                          | int *NULL* [**0**]     |      |
| physicalinterface_name                        | varchar(255) *NULL* [] |      |
| physicalinterface_device_id                   | int *NULL* [**0**]     |      |
| physicalinterface_device_name                 | varchar(255) *NULL* [] |      |
| vlan_id                                       | int *NULL* [**0**]     |      |
| vlan_tag                                      | varchar(255) *NULL* [] |      |
| friendlyname                                  | varchar(23) *NULL*     |      |
| physicalinterface_id_friendlyname             | varchar(511) *NULL*    |      |
| physicalinterface_id_obsolescence_flag        | int [**0**]            |      |
| physicalinterface_device_id_friendlyname      | varchar(255) *NULL*    |      |
| physicalinterface_device_id_obsolescence_flag | int [**0**]            |      |
| vlan_id_friendlyname                          | varchar(255) *NULL*    |      |

```
SELECT DISTINCT
	`lnkPhysicalInterfaceToVLAN`.`id` AS `id`,
	`lnkPhysicalInterfaceToVLAN`.`physicalinterface_id` AS `physicalinterface_id`,
	`PhysicalInterface_physicalinterface_id_NetworkInterface`.`name` AS `physicalinterface_name`,
	`PhysicalInterface_physicalinterface_id`.`connectableci_id` AS `physicalinterface_device_id`,
	`ConnectableCI_connectableci_id_FunctionalCI`.`name` AS `physicalinterface_device_name`,
	`lnkPhysicalInterfaceToVLAN`.`vlan_id` AS `vlan_id`,
	`VLAN_vlan_id`.`vlan_tag` AS `vlan_tag`,
	cast(
		concat(
			COALESCE ( `lnkPhysicalInterfaceToVLAN`.`physicalinterface_id`, '' ),
			COALESCE ( ' ', '' ),
		COALESCE ( `lnkPhysicalInterfaceToVLAN`.`vlan_id`, '' )) AS CHAR charset utf8mb4 
	) AS `friendlyname`,
	cast(
		concat(
			COALESCE ( `PhysicalInterface_physicalinterface_id_NetworkInterface`.`name`, '' ),
			COALESCE ( ' ', '' ),
		COALESCE ( `ConnectableCI_connectableci_id_FunctionalCI`.`name`, '' )) AS CHAR charset utf8mb4 
	) AS `physicalinterface_id_friendlyname`,
	COALESCE ( COALESCE (( `ConnectableCI_connectableci_id_PhysicalDevice`.`status` = 'obsolete' ), 0 ), 0 ) AS `physicalinterface_id_obsolescence_flag`,
	cast( concat( COALESCE ( `ConnectableCI_connectableci_id_FunctionalCI`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `physicalinterface_device_id_friendlyname`,
	COALESCE (( `ConnectableCI_connectableci_id_PhysicalDevice`.`status` = 'obsolete' ), 0 ) AS `physicalinterface_device_id_obsolescence_flag`,
	cast( concat( COALESCE ( `VLAN_vlan_id`.`vlan_tag`, '' )) AS CHAR charset utf8mb4 ) AS `vlan_id_friendlyname` 
FROM
	((
			`lnkphysicalinterfacetovlan` `lnkPhysicalInterfaceToVLAN`
			JOIN ((
					`physicalinterface` `PhysicalInterface_physicalinterface_id`
					JOIN (
						`physicaldevice` `ConnectableCI_connectableci_id_PhysicalDevice`
						JOIN `functionalci` `ConnectableCI_connectableci_id_FunctionalCI` ON ((
								`ConnectableCI_connectableci_id_PhysicalDevice`.`id` = `ConnectableCI_connectableci_id_FunctionalCI`.`id` 
								))) ON ((
							`PhysicalInterface_physicalinterface_id`.`connectableci_id` = `ConnectableCI_connectableci_id_PhysicalDevice`.`id` 
						)))
				JOIN `networkinterface` `PhysicalInterface_physicalinterface_id_NetworkInterface` ON ((
						`PhysicalInterface_physicalinterface_id`.`id` = `PhysicalInterface_physicalinterface_id_NetworkInterface`.`id` 
						))) ON ((
					`lnkPhysicalInterfaceToVLAN`.`physicalinterface_id` = `PhysicalInterface_physicalinterface_id`.`id` 
				)))
		JOIN `vlan` `VLAN_vlan_id` ON ((
				`lnkPhysicalInterfaceToVLAN`.`vlan_id` = `VLAN_vlan_id`.`id` 
			))) 
WHERE
	(
	0 <> COALESCE (( `ConnectableCI_connectableci_id_PhysicalDevice`.`finalclass` IN ( 'DatacenterDevice', 'NetworkDevice', 'Server', 'PC', 'Printer', 'StorageSystem', 'SANSwitch', 'TapeLibrary', 'NAS', 'ConnectableCI' )), 1 ))
```

