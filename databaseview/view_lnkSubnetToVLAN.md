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
select distinct `lnkSubnetToVLAN`.`id` AS `id`,`lnkSubnetToVLAN`.`subnet_id` AS `subnet_id`,`Subnet_subnet_id`.`ip` AS `subnet_ip`,`Subnet_subnet_id`.`subnet_name` AS `subnet_name`,`lnkSubnetToVLAN`.`vlan_id` AS `vlan_id`,`VLAN_vlan_id`.`vlan_tag` AS `vlan_tag`,cast(concat(coalesce(`lnkSubnetToVLAN`.`subnet_id`,''),coalesce(' ',''),coalesce(`lnkSubnetToVLAN`.`vlan_id`,'')) as char charset utf8mb4) AS `friendlyname`,cast(concat(coalesce(`Subnet_subnet_id`.`ip`,''),coalesce(' ',''),coalesce(`Subnet_subnet_id`.`ip_mask`,'')) as char charset utf8mb4) AS `subnet_id_friendlyname`,cast(concat(coalesce(`VLAN_vlan_id`.`vlan_tag`,'')) as char charset utf8mb4) AS `vlan_id_friendlyname` from ((`lnksubnettovlan` `lnkSubnetToVLAN` join `subnet` `Subnet_subnet_id` on((`lnkSubnetToVLAN`.`subnet_id` = `Subnet_subnet_id`.`id`))) join `vlan` `VLAN_vlan_id` on((`lnkSubnetToVLAN`.`vlan_id` = `VLAN_vlan_id`.`id`))) where (0 <> 1)
```

