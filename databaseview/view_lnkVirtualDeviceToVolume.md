| 列                                 | 类型                                   | 注释 |
| :--------------------------------- | -------------------------------------- | ---- |
| id                                 | int [**0**]                            |      |
| volume_id                          | int *NULL* [**0**]                     |      |
| volume_name                        | varchar(255) *NULL* []                 |      |
| virtualdevice_id                   | int *NULL* [**0**]                     |      |
| virtualdevice_name                 | varchar(255) *NULL* []                 |      |
| size_used                          | varchar(255) *NULL* []                 |      |
| friendlyname                       | varchar(11) *NULL*                     |      |
| volume_id_friendlyname             | varchar(511) *NULL*                    |      |
| volume_id_obsolescence_flag        | int [**0**]                            |      |
| virtualdevice_id_friendlyname      | varchar(255) *NULL*                    |      |
| virtualdevice_id_finalclass_recall | varchar(255) *NULL* [**FunctionalCI**] |      |
| virtualdevice_id_obsolescence_flag | int [**0**]                            |      |

```
SELECT DISTINCT
	`lnkVirtualDeviceToVolume`.`id` AS `id`,
	`lnkVirtualDeviceToVolume`.`volume_id` AS `volume_id`,
	`LogicalVolume_volume_id`.`name` AS `volume_name`,
	`lnkVirtualDeviceToVolume`.`virtualdevice_id` AS `virtualdevice_id`,
	`VirtualDevice_virtualdevice_id_FunctionalCI`.`name` AS `virtualdevice_name`,
	`lnkVirtualDeviceToVolume`.`size_used` AS `size_used`,
	cast( concat( COALESCE ( `lnkVirtualDeviceToVolume`.`volume_id`, '' )) AS CHAR charset utf8mb4 ) AS `friendlyname`,
	cast(
		concat(
			COALESCE ( `StorageSystem_storagesystem_id_FunctionalCI`.`name`, '' ),
			COALESCE ( ' ', '' ),
		COALESCE ( `LogicalVolume_volume_id`.`name`, '' )) AS CHAR charset utf8mb4 
	) AS `volume_id_friendlyname`,
	COALESCE ( COALESCE (( `StorageSystem_storagesystem_id_PhysicalDevice`.`status` = 'obsolete' ), 0 ), 0 ) AS `volume_id_obsolescence_flag`,
	cast( concat( COALESCE ( `VirtualDevice_virtualdevice_id_FunctionalCI`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `virtualdevice_id_friendlyname`,
	`VirtualDevice_virtualdevice_id_FunctionalCI`.`finalclass` AS `virtualdevice_id_finalclass_recall`,
	COALESCE (( `VirtualDevice_virtualdevice_id`.`status` = 'obsolete' ), 0 ) AS `virtualdevice_id_obsolescence_flag` 
FROM
	((
			`lnkvirtualdevicetovolume` `lnkVirtualDeviceToVolume`
			JOIN (
				`logicalvolume` `LogicalVolume_volume_id`
				JOIN (
					`physicaldevice` `StorageSystem_storagesystem_id_PhysicalDevice`
					JOIN `functionalci` `StorageSystem_storagesystem_id_FunctionalCI` ON ((
							`StorageSystem_storagesystem_id_PhysicalDevice`.`id` = `StorageSystem_storagesystem_id_FunctionalCI`.`id` 
							))) ON ((
						`LogicalVolume_volume_id`.`storagesystem_id` = `StorageSystem_storagesystem_id_PhysicalDevice`.`id` 
					))) ON ((
					`lnkVirtualDeviceToVolume`.`volume_id` = `LogicalVolume_volume_id`.`id` 
				)))
		JOIN (
			`virtualdevice` `VirtualDevice_virtualdevice_id`
			JOIN `functionalci` `VirtualDevice_virtualdevice_id_FunctionalCI` ON ((
					`VirtualDevice_virtualdevice_id`.`id` = `VirtualDevice_virtualdevice_id_FunctionalCI`.`id` 
					))) ON ((
				`lnkVirtualDeviceToVolume`.`virtualdevice_id` = `VirtualDevice_virtualdevice_id`.`id` 
			))) 
WHERE
	(
	0 <> COALESCE (( `StorageSystem_storagesystem_id_PhysicalDevice`.`finalclass` = 'StorageSystem' ), 1 ))
```

