| 列                                    | 类型                                   | 注释 |
| :------------------------------------ | -------------------------------------- | ---- |
| id                                    | int [**0**]                            |      |
| san_id                                | int *NULL* [**0**]                     |      |
| san_name                              | varchar(255) *NULL* []                 |      |
| datacenterdevice_id                   | int *NULL* [**0**]                     |      |
| datacenterdevice_name                 | varchar(255) *NULL* []                 |      |
| san_port                              | varchar(255) *NULL* []                 |      |
| datacenterdevice_port                 | varchar(255) *NULL* []                 |      |
| friendlyname                          | varchar(11) *NULL*                     |      |
| san_id_friendlyname                   | varchar(255) *NULL*                    |      |
| san_id_obsolescence_flag              | int [**0**]                            |      |
| datacenterdevice_id_friendlyname      | varchar(255) *NULL*                    |      |
| datacenterdevice_id_finalclass_recall | varchar(255) *NULL* [**FunctionalCI**] |      |
| datacenterdevice_id_obsolescence_flag | int [**0**]                            |      |

```
SELECT DISTINCT
	`lnkSanToDatacenterDevice`.`id` AS `id`,
	`lnkSanToDatacenterDevice`.`san_id` AS `san_id`,
	`SANSwitch_san_id_FunctionalCI`.`name` AS `san_name`,
	`lnkSanToDatacenterDevice`.`datacenterdevice_id` AS `datacenterdevice_id`,
	`DatacenterDevice_datacenterdevice_id_FunctionalCI`.`name` AS `datacenterdevice_name`,
	`lnkSanToDatacenterDevice`.`san_port` AS `san_port`,
	`lnkSanToDatacenterDevice`.`datacenterdevice_port` AS `datacenterdevice_port`,
	cast( concat( COALESCE ( `lnkSanToDatacenterDevice`.`san_id`, '' )) AS CHAR charset utf8mb4 ) AS `friendlyname`,
	cast( concat( COALESCE ( `SANSwitch_san_id_FunctionalCI`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `san_id_friendlyname`,
	COALESCE (( `SANSwitch_san_id_PhysicalDevice`.`status` = 'obsolete' ), 0 ) AS `san_id_obsolescence_flag`,
	cast( concat( COALESCE ( `DatacenterDevice_datacenterdevice_id_FunctionalCI`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `datacenterdevice_id_friendlyname`,
	`DatacenterDevice_datacenterdevice_id_FunctionalCI`.`finalclass` AS `datacenterdevice_id_finalclass_recall`,
	COALESCE (( `DatacenterDevice_datacenterdevice_id_PhysicalDevice`.`status` = 'obsolete' ), 0 ) AS `datacenterdevice_id_obsolescence_flag` 
FROM
	((
			`lnkdatacenterdevicetosan` `lnkSanToDatacenterDevice`
			JOIN (
				`physicaldevice` `SANSwitch_san_id_PhysicalDevice`
				JOIN `functionalci` `SANSwitch_san_id_FunctionalCI` ON ((
						`SANSwitch_san_id_PhysicalDevice`.`id` = `SANSwitch_san_id_FunctionalCI`.`id` 
						))) ON ((
					`lnkSanToDatacenterDevice`.`san_id` = `SANSwitch_san_id_PhysicalDevice`.`id` 
				)))
		JOIN (
			`physicaldevice` `DatacenterDevice_datacenterdevice_id_PhysicalDevice`
			JOIN `functionalci` `DatacenterDevice_datacenterdevice_id_FunctionalCI` ON ((
					`DatacenterDevice_datacenterdevice_id_PhysicalDevice`.`id` = `DatacenterDevice_datacenterdevice_id_FunctionalCI`.`id` 
					))) ON ((
				`lnkSanToDatacenterDevice`.`datacenterdevice_id` = `DatacenterDevice_datacenterdevice_id_PhysicalDevice`.`id` 
			))) 
WHERE
	((
			0 <> COALESCE (( `SANSwitch_san_id_PhysicalDevice`.`finalclass` = 'SANSwitch' ), 1 )) 
	AND (
	0 <> COALESCE (( `DatacenterDevice_datacenterdevice_id_PhysicalDevice`.`finalclass` IN ( 'NetworkDevice', 'Server', 'StorageSystem', 'SANSwitch', 'TapeLibrary', 'NAS', 'DatacenterDevice' )), 1 )))
```

