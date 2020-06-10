| 列                          | 类型                   | 注释 |
| :-------------------------- | ---------------------- | ---- |
| id                          | int [**0**]            |      |
| volume_id                   | int *NULL* [**0**]     |      |
| volume_name                 | varchar(255) *NULL* [] |      |
| server_id                   | int *NULL* [**0**]     |      |
| server_name                 | varchar(255) *NULL* [] |      |
| size_used                   | varchar(255) *NULL* [] |      |
| friendlyname                | varchar(11) *NULL*     |      |
| volume_id_friendlyname      | varchar(511) *NULL*    |      |
| volume_id_obsolescence_flag | int [**0**]            |      |
| server_id_friendlyname      | varchar(255) *NULL*    |      |
| server_id_obsolescence_flag | int [**0**]            |      |

```
SELECT DISTINCT
	`lnkServerToVolume`.`id` AS `id`,
	`lnkServerToVolume`.`volume_id` AS `volume_id`,
	`LogicalVolume_volume_id`.`name` AS `volume_name`,
	`lnkServerToVolume`.`server_id` AS `server_id`,
	`Server_server_id_FunctionalCI`.`name` AS `server_name`,
	`lnkServerToVolume`.`size_used` AS `size_used`,
	cast( concat( COALESCE ( `lnkServerToVolume`.`volume_id`, '' )) AS CHAR charset utf8mb4 ) AS `friendlyname`,
	cast(
		concat(
			COALESCE ( `StorageSystem_storagesystem_id_FunctionalCI`.`name`, '' ),
			COALESCE ( ' ', '' ),
		COALESCE ( `LogicalVolume_volume_id`.`name`, '' )) AS CHAR charset utf8mb4 
	) AS `volume_id_friendlyname`,
	COALESCE ( COALESCE (( `StorageSystem_storagesystem_id_PhysicalDevice`.`status` = 'obsolete' ), 0 ), 0 ) AS `volume_id_obsolescence_flag`,
	cast( concat( COALESCE ( `Server_server_id_FunctionalCI`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `server_id_friendlyname`,
	COALESCE (( `Server_server_id_PhysicalDevice`.`status` = 'obsolete' ), 0 ) AS `server_id_obsolescence_flag` 
FROM
	((
			`lnkservertovolume` `lnkServerToVolume`
			JOIN (
				`logicalvolume` `LogicalVolume_volume_id`
				JOIN (
					`physicaldevice` `StorageSystem_storagesystem_id_PhysicalDevice`
					JOIN `functionalci` `StorageSystem_storagesystem_id_FunctionalCI` ON ((
							`StorageSystem_storagesystem_id_PhysicalDevice`.`id` = `StorageSystem_storagesystem_id_FunctionalCI`.`id` 
							))) ON ((
						`LogicalVolume_volume_id`.`storagesystem_id` = `StorageSystem_storagesystem_id_PhysicalDevice`.`id` 
					))) ON ((
					`lnkServerToVolume`.`volume_id` = `LogicalVolume_volume_id`.`id` 
				)))
		JOIN (
			`physicaldevice` `Server_server_id_PhysicalDevice`
			JOIN `functionalci` `Server_server_id_FunctionalCI` ON ((
					`Server_server_id_PhysicalDevice`.`id` = `Server_server_id_FunctionalCI`.`id` 
					))) ON ((
				`lnkServerToVolume`.`server_id` = `Server_server_id_PhysicalDevice`.`id` 
			))) 
WHERE
	((
			0 <> COALESCE (( `StorageSystem_storagesystem_id_PhysicalDevice`.`finalclass` = 'StorageSystem' ), 1 )) 
	AND (
	0 <> COALESCE (( `Server_server_id_PhysicalDevice`.`finalclass` = 'Server' ), 1 )))
```

