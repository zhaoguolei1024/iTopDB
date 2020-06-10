| 列                                 | 类型                                            | 注释 |
| :--------------------------------- | ----------------------------------------------- | ---- |
| id                                 | int [**0**]                                     |      |
| networkdevice_id                   | int *NULL* [**0**]                              |      |
| networkdevice_name                 | varchar(255) *NULL* []                          |      |
| connectableci_id                   | int *NULL* [**0**]                              |      |
| connectableci_name                 | varchar(255) *NULL* []                          |      |
| network_port                       | varchar(255) *NULL* []                          |      |
| device_port                        | varchar(255) *NULL* []                          |      |
| connection_type                    | enum('downlink','uplink') *NULL* [**downlink**] |      |
| friendlyname                       | varchar(23) *NULL*                              |      |
| networkdevice_id_friendlyname      | varchar(255) *NULL*                             |      |
| networkdevice_id_obsolescence_flag | int [**0**]                                     |      |
| connectableci_id_friendlyname      | varchar(255) *NULL*                             |      |
| connectableci_id_finalclass_recall | varchar(255) *NULL* [**FunctionalCI**]          |      |
| connectableci_id_obsolescence_flag | int [**0**]                                     |      |

```
SELECT DISTINCT
	`lnkConnectableCIToNetworkDevice`.`id` AS `id`,
	`lnkConnectableCIToNetworkDevice`.`networkdevice_id` AS `networkdevice_id`,
	`NetworkDevice_networkdevice_id_FunctionalCI`.`name` AS `networkdevice_name`,
	`lnkConnectableCIToNetworkDevice`.`connectableci_id` AS `connectableci_id`,
	`ConnectableCI_connectableci_id_FunctionalCI`.`name` AS `connectableci_name`,
	`lnkConnectableCIToNetworkDevice`.`network_port` AS `network_port`,
	`lnkConnectableCIToNetworkDevice`.`device_port` AS `device_port`,
	`lnkConnectableCIToNetworkDevice`.`type` AS `connection_type`,
	cast(
		concat(
			COALESCE ( `lnkConnectableCIToNetworkDevice`.`networkdevice_id`, '' ),
			COALESCE ( ' ', '' ),
		COALESCE ( `lnkConnectableCIToNetworkDevice`.`connectableci_id`, '' )) AS CHAR charset utf8mb4 
	) AS `friendlyname`,
	cast( concat( COALESCE ( `NetworkDevice_networkdevice_id_FunctionalCI`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `networkdevice_id_friendlyname`,
	COALESCE (( `NetworkDevice_networkdevice_id_PhysicalDevice`.`status` = 'obsolete' ), 0 ) AS `networkdevice_id_obsolescence_flag`,
	cast( concat( COALESCE ( `ConnectableCI_connectableci_id_FunctionalCI`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `connectableci_id_friendlyname`,
	`ConnectableCI_connectableci_id_FunctionalCI`.`finalclass` AS `connectableci_id_finalclass_recall`,
	COALESCE (( `ConnectableCI_connectableci_id_PhysicalDevice`.`status` = 'obsolete' ), 0 ) AS `connectableci_id_obsolescence_flag` 
FROM
	((
			`lnkconnectablecitonetworkdevice` `lnkConnectableCIToNetworkDevice`
			JOIN (
				`physicaldevice` `NetworkDevice_networkdevice_id_PhysicalDevice`
				JOIN `functionalci` `NetworkDevice_networkdevice_id_FunctionalCI` ON ((
						`NetworkDevice_networkdevice_id_PhysicalDevice`.`id` = `NetworkDevice_networkdevice_id_FunctionalCI`.`id` 
						))) ON ((
					`lnkConnectableCIToNetworkDevice`.`networkdevice_id` = `NetworkDevice_networkdevice_id_PhysicalDevice`.`id` 
				)))
		JOIN (
			`physicaldevice` `ConnectableCI_connectableci_id_PhysicalDevice`
			JOIN `functionalci` `ConnectableCI_connectableci_id_FunctionalCI` ON ((
					`ConnectableCI_connectableci_id_PhysicalDevice`.`id` = `ConnectableCI_connectableci_id_FunctionalCI`.`id` 
					))) ON ((
				`lnkConnectableCIToNetworkDevice`.`connectableci_id` = `ConnectableCI_connectableci_id_PhysicalDevice`.`id` 
			))) 
WHERE
	((
			0 <> COALESCE (( `NetworkDevice_networkdevice_id_PhysicalDevice`.`finalclass` = 'NetworkDevice' ), 1 )) 
	AND (
	0 <> COALESCE (( `ConnectableCI_connectableci_id_PhysicalDevice`.`finalclass` IN ( 'DatacenterDevice', 'NetworkDevice', 'Server', 'PC', 'Printer', 'StorageSystem', 'SANSwitch', 'TapeLibrary', 'NAS', 'ConnectableCI' )), 1 )))
```

