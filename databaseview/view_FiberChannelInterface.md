| 列                                    | 类型                                       | 注释 |
| :------------------------------------ | ------------------------------------------ | ---- |
| id                                    | int [**0**]                                |      |
| name                                  | varchar(255) *NULL* []                     |      |
| speed                                 | decimal(6,2) *NULL*                        |      |
| topology                              | varchar(255) *NULL* []                     |      |
| wwn                                   | varchar(255) *NULL* []                     |      |
| datacenterdevice_id                   | int *NULL* [**0**]                         |      |
| datacenterdevice_name                 | varchar(255) *NULL* []                     |      |
| finalclass                            | varchar(255) *NULL* [**NetworkInterface**] |      |
| friendlyname                          | varchar(511) *NULL*                        |      |
| obsolescence_flag                     | int [**0**]                                |      |
| obsolescence_date                     | date *NULL*                                |      |
| datacenterdevice_id_friendlyname      | varchar(255) *NULL*                        |      |
| datacenterdevice_id_finalclass_recall | varchar(255) *NULL* [**FunctionalCI**]     |      |
| datacenterdevice_id_obsolescence_flag | int [**0**]                                |      |

```
SELECT DISTINCT
	`FiberChannelInterface`.`id` AS `id`,
	`FiberChannelInterface_NetworkInterface`.`name` AS `name`,
	`FiberChannelInterface`.`speed` AS `speed`,
	`FiberChannelInterface`.`topology` AS `topology`,
	`FiberChannelInterface`.`wwn` AS `wwn`,
	`FiberChannelInterface`.`datacenterdevice_id` AS `datacenterdevice_id`,
	`DatacenterDevice_datacenterdevice_id_FunctionalCI`.`name` AS `datacenterdevice_name`,
	`FiberChannelInterface_NetworkInterface`.`finalclass` AS `finalclass`,
	cast(
		concat(
			COALESCE ( `FiberChannelInterface_NetworkInterface`.`name`, '' ),
			COALESCE ( ' ', '' ),
		COALESCE ( `DatacenterDevice_datacenterdevice_id_FunctionalCI`.`name`, '' )) AS CHAR charset utf8mb4 
	) AS `friendlyname`,
	COALESCE ( COALESCE (( `DatacenterDevice_datacenterdevice_id_PhysicalDevice`.`status` = 'obsolete' ), 0 ), 0 ) AS `obsolescence_flag`,
	`FiberChannelInterface_NetworkInterface`.`obsolescence_date` AS `obsolescence_date`,
	cast( concat( COALESCE ( `DatacenterDevice_datacenterdevice_id_FunctionalCI`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `datacenterdevice_id_friendlyname`,
	`DatacenterDevice_datacenterdevice_id_FunctionalCI`.`finalclass` AS `datacenterdevice_id_finalclass_recall`,
	COALESCE (( `DatacenterDevice_datacenterdevice_id_PhysicalDevice`.`status` = 'obsolete' ), 0 ) AS `datacenterdevice_id_obsolescence_flag` 
FROM
	((
			`fiberchannelinterface` `FiberChannelInterface`
			JOIN (
				`physicaldevice` `DatacenterDevice_datacenterdevice_id_PhysicalDevice`
				JOIN `functionalci` `DatacenterDevice_datacenterdevice_id_FunctionalCI` ON ((
						`DatacenterDevice_datacenterdevice_id_PhysicalDevice`.`id` = `DatacenterDevice_datacenterdevice_id_FunctionalCI`.`id` 
						))) ON ((
					`FiberChannelInterface`.`datacenterdevice_id` = `DatacenterDevice_datacenterdevice_id_PhysicalDevice`.`id` 
				)))
		JOIN `networkinterface` `FiberChannelInterface_NetworkInterface` ON ((
				`FiberChannelInterface`.`id` = `FiberChannelInterface_NetworkInterface`.`id` 
			))) 
WHERE
	(
	0 <> COALESCE (( `DatacenterDevice_datacenterdevice_id_PhysicalDevice`.`finalclass` IN ( 'NetworkDevice', 'Server', 'StorageSystem', 'SANSwitch', 'TapeLibrary', 'NAS', 'DatacenterDevice' )), 1 ))
```

