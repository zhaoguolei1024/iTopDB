| 列                     | 类型                   | 注释 |
| :--------------------- | ---------------------- | ---- |
| id                     | int [**0**]            |      |
| subnet_id              | int *NULL* [**0**]     |      |
| subnet_ip              | varchar(255) *NULL* [] |      |
| subnet_name            | varchar(255) *NULL* [] |      |
| vlan_id                | int *NULL* [**0**]     |      |
| vlan_tag               | varchar(255) *NULL* [] |      |
| friendlyname           | varchar(23) *NULL*     |      |
| subnet_id_friendlyname | varchar(511) *NULL*    |      |
| vlan_id_friendlyname   | varchar(255) *NULL*    |      |

```
SELECT DISTINCT
	`lnkSubnetToVLAN`.`id` AS `id`,
	`lnkSubnetToVLAN`.`subnet_id` AS `subnet_id`,
	`Subnet_subnet_id`.`ip` AS `subnet_ip`,
	`Subnet_subnet_id`.`subnet_name` AS `subnet_name`,
	`lnkSubnetToVLAN`.`vlan_id` AS `vlan_id`,
	`VLAN_vlan_id`.`vlan_tag` AS `vlan_tag`,
	cast(
		concat(
			COALESCE ( `lnkSubnetToVLAN`.`subnet_id`, '' ),
			COALESCE ( ' ', '' ),
		COALESCE ( `lnkSubnetToVLAN`.`vlan_id`, '' )) AS CHAR charset utf8mb4 
	) AS `friendlyname`,
	cast(
		concat(
			COALESCE ( `Subnet_subnet_id`.`ip`, '' ),
			COALESCE ( ' ', '' ),
		COALESCE ( `Subnet_subnet_id`.`ip_mask`, '' )) AS CHAR charset utf8mb4 
	) AS `subnet_id_friendlyname`,
	cast( concat( COALESCE ( `VLAN_vlan_id`.`vlan_tag`, '' )) AS CHAR charset utf8mb4 ) AS `vlan_id_friendlyname` 
FROM
	((
			`lnksubnettovlan` `lnkSubnetToVLAN`
			JOIN `subnet` `Subnet_subnet_id` ON ((
					`lnkSubnetToVLAN`.`subnet_id` = `Subnet_subnet_id`.`id` 
				)))
		JOIN `vlan` `VLAN_vlan_id` ON ((
				`lnkSubnetToVLAN`.`vlan_id` = `VLAN_vlan_id`.`id` 
			))) 
WHERE
	(
	0 <> 1)
```

