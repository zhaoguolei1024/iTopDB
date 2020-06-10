| 列                                    | 类型                                   | 注释 |
| :------------------------------------ | -------------------------------------- | ---- |
| id                                    | int [**0**]                            |      |
| softwarepatch_id                      | int *NULL* [**0**]                     |      |
| softwarepatch_name                    | varchar(255) *NULL* []                 |      |
| softwareinstance_id                   | int *NULL* [**0**]                     |      |
| softwareinstance_name                 | varchar(255) *NULL* []                 |      |
| friendlyname                          | varchar(23) *NULL*                     |      |
| softwarepatch_id_friendlyname         | varchar(255) *NULL*                    |      |
| softwareinstance_id_friendlyname      | varchar(511) *NULL*                    |      |
| softwareinstance_id_finalclass_recall | varchar(255) *NULL* [**FunctionalCI**] |      |
| softwareinstance_id_obsolescence_flag | int [**0**]                            |      |

```
SELECT DISTINCT
	`lnkSoftwareInstanceToSoftwarePatch`.`id` AS `id`,
	`lnkSoftwareInstanceToSoftwarePatch`.`softwarepatch_id` AS `softwarepatch_id`,
	`SoftwarePatch_softwarepatch_id_Patch`.`name` AS `softwarepatch_name`,
	`lnkSoftwareInstanceToSoftwarePatch`.`softwareinstance_id` AS `softwareinstance_id`,
	`SoftwareInstance_softwareinstance_id_FunctionalCI`.`name` AS `softwareinstance_name`,
	cast(
		concat(
			COALESCE ( `lnkSoftwareInstanceToSoftwarePatch`.`softwarepatch_id`, '' ),
			COALESCE ( ' ', '' ),
		COALESCE ( `lnkSoftwareInstanceToSoftwarePatch`.`softwareinstance_id`, '' )) AS CHAR charset utf8mb4 
	) AS `friendlyname`,
	cast( concat( COALESCE ( `SoftwarePatch_softwarepatch_id_Patch`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `softwarepatch_id_friendlyname`,
	cast(
		concat(
			COALESCE ( `SoftwareInstance_softwareinstance_id_FunctionalCI`.`name`, '' ),
			COALESCE ( ' ', '' ),
		COALESCE ( `FunctionalCI_system_id`.`name`, '' )) AS CHAR charset utf8mb4 
	) AS `softwareinstance_id_friendlyname`,
	`SoftwareInstance_softwareinstance_id_FunctionalCI`.`finalclass` AS `softwareinstance_id_finalclass_recall`,
	COALESCE (( `SoftwareInstance_softwareinstance_id`.`status` = 'inactive' ), 0 ) AS `softwareinstance_id_obsolescence_flag` 
FROM
	((
			`lnksoftwareinstancetosoftwarepatch` `lnkSoftwareInstanceToSoftwarePatch`
			JOIN `patch` `SoftwarePatch_softwarepatch_id_Patch` ON ((
					`lnkSoftwareInstanceToSoftwarePatch`.`softwarepatch_id` = `SoftwarePatch_softwarepatch_id_Patch`.`id` 
				)))
		JOIN ((
				`softwareinstance` `SoftwareInstance_softwareinstance_id`
				JOIN `functionalci` `FunctionalCI_system_id` ON ((
						`SoftwareInstance_softwareinstance_id`.`functionalci_id` = `FunctionalCI_system_id`.`id` 
					)))
			JOIN `functionalci` `SoftwareInstance_softwareinstance_id_FunctionalCI` ON ((
					`SoftwareInstance_softwareinstance_id`.`id` = `SoftwareInstance_softwareinstance_id_FunctionalCI`.`id` 
					))) ON ((
				`lnkSoftwareInstanceToSoftwarePatch`.`softwareinstance_id` = `SoftwareInstance_softwareinstance_id`.`id` 
			))) 
WHERE
	(
	0 <> COALESCE (( `SoftwarePatch_softwarepatch_id_Patch`.`finalclass` = 'SoftwarePatch' ), 1 ))
```

