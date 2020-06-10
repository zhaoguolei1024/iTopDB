| 列                                  | 类型                                       | 注释 |
| :---------------------------------- | ------------------------------------------ | ---- |
| id                                  | int [**0**]                                |      |
| name                                | varchar(255) *NULL* []                     |      |
| ipaddress                           | varchar(255) *NULL* []                     |      |
| macaddress                          | varchar(255) *NULL* []                     |      |
| comment                             | text *NULL*                                |      |
| ipgateway                           | varchar(255) *NULL* []                     |      |
| ipmask                              | varchar(255) *NULL* []                     |      |
| speed                               | decimal(12,2) *NULL*                       |      |
| virtualmachine_id                   | int *NULL* [**0**]                         |      |
| virtualmachine_name                 | varchar(255) *NULL* []                     |      |
| finalclass                          | varchar(255) *NULL* [**NetworkInterface**] |      |
| friendlyname                        | varchar(511) *NULL*                        |      |
| obsolescence_flag                   | int [**0**]                                |      |
| obsolescence_date                   | date *NULL*                                |      |
| virtualmachine_id_friendlyname      | varchar(255) *NULL*                        |      |
| virtualmachine_id_obsolescence_flag | int [**0**]                                |      |

```
SELECT DISTINCT
	`LogicalInterface`.`id` AS `id`,
	`LogicalInterface_NetworkInterface`.`name` AS `name`,
	`LogicalInterface_IPInterface`.`ipaddress` AS `ipaddress`,
	`LogicalInterface_IPInterface`.`macaddress` AS `macaddress`,
	`LogicalInterface_IPInterface`.`comment` AS `comment`,
	`LogicalInterface_IPInterface`.`ipgateway` AS `ipgateway`,
	`LogicalInterface_IPInterface`.`ipmask` AS `ipmask`,
	`LogicalInterface_IPInterface`.`speed` AS `speed`,
	`LogicalInterface`.`virtualmachine_id` AS `virtualmachine_id`,
	`VirtualMachine_virtualmachine_id_FunctionalCI`.`name` AS `virtualmachine_name`,
	`LogicalInterface_NetworkInterface`.`finalclass` AS `finalclass`,
	cast(
		concat(
			COALESCE ( `LogicalInterface_NetworkInterface`.`name`, '' ),
			COALESCE ( ' ', '' ),
		COALESCE ( `VirtualMachine_virtualmachine_id_FunctionalCI`.`name`, '' )) AS CHAR charset utf8mb4 
	) AS `friendlyname`,
	COALESCE ( COALESCE (( `VirtualMachine_virtualmachine_id_VirtualDevice`.`status` = 'obsolete' ), 0 ), 0 ) AS `obsolescence_flag`,
	`LogicalInterface_NetworkInterface`.`obsolescence_date` AS `obsolescence_date`,
	cast( concat( COALESCE ( `VirtualMachine_virtualmachine_id_FunctionalCI`.`name`, '' )) AS CHAR charset utf8mb4 ) AS `virtualmachine_id_friendlyname`,
	COALESCE (( `VirtualMachine_virtualmachine_id_VirtualDevice`.`status` = 'obsolete' ), 0 ) AS `virtualmachine_id_obsolescence_flag` 
FROM
	(((
				`logicalinterface` `LogicalInterface`
				JOIN (
					`virtualdevice` `VirtualMachine_virtualmachine_id_VirtualDevice`
					JOIN `functionalci` `VirtualMachine_virtualmachine_id_FunctionalCI` ON ((
							`VirtualMachine_virtualmachine_id_VirtualDevice`.`id` = `VirtualMachine_virtualmachine_id_FunctionalCI`.`id` 
							))) ON ((
						`LogicalInterface`.`virtualmachine_id` = `VirtualMachine_virtualmachine_id_VirtualDevice`.`id` 
					)))
			JOIN `ipinterface` `LogicalInterface_IPInterface` ON ((
					`LogicalInterface`.`id` = `LogicalInterface_IPInterface`.`id` 
				)))
		JOIN `networkinterface` `LogicalInterface_NetworkInterface` ON ((
				`LogicalInterface`.`id` = `LogicalInterface_NetworkInterface`.`id` 
			))) 
WHERE
	(
	0 <> COALESCE (( `VirtualMachine_virtualmachine_id_VirtualDevice`.`finalclass` = 'VirtualMachine' ), 1 ))
```

