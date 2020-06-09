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
select distinct `LogicalInterface`.`id` AS `id`,`LogicalInterface_NetworkInterface`.`name` AS `name`,`LogicalInterface_IPInterface`.`ipaddress` AS `ipaddress`,`LogicalInterface_IPInterface`.`macaddress` AS `macaddress`,`LogicalInterface_IPInterface`.`comment` AS `comment`,`LogicalInterface_IPInterface`.`ipgateway` AS `ipgateway`,`LogicalInterface_IPInterface`.`ipmask` AS `ipmask`,`LogicalInterface_IPInterface`.`speed` AS `speed`,`LogicalInterface`.`virtualmachine_id` AS `virtualmachine_id`,`VirtualMachine_virtualmachine_id_FunctionalCI`.`name` AS `virtualmachine_name`,`LogicalInterface_NetworkInterface`.`finalclass` AS `finalclass`,cast(concat(coalesce(`LogicalInterface_NetworkInterface`.`name`,''),coalesce(' ',''),coalesce(`VirtualMachine_virtualmachine_id_FunctionalCI`.`name`,'')) as char charset utf8mb4) AS `friendlyname`,coalesce(coalesce((`VirtualMachine_virtualmachine_id_VirtualDevice`.`status` = 'obsolete'),0),0) AS `obsolescence_flag`,`LogicalInterface_NetworkInterface`.`obsolescence_date` AS `obsolescence_date`,cast(concat(coalesce(`VirtualMachine_virtualmachine_id_FunctionalCI`.`name`,'')) as char charset utf8mb4) AS `virtualmachine_id_friendlyname`,coalesce((`VirtualMachine_virtualmachine_id_VirtualDevice`.`status` = 'obsolete'),0) AS `virtualmachine_id_obsolescence_flag` from (((`logicalinterface` `LogicalInterface` join (`virtualdevice` `VirtualMachine_virtualmachine_id_VirtualDevice` join `functionalci` `VirtualMachine_virtualmachine_id_FunctionalCI` on((`VirtualMachine_virtualmachine_id_VirtualDevice`.`id` = `VirtualMachine_virtualmachine_id_FunctionalCI`.`id`))) on((`LogicalInterface`.`virtualmachine_id` = `VirtualMachine_virtualmachine_id_VirtualDevice`.`id`))) join `ipinterface` `LogicalInterface_IPInterface` on((`LogicalInterface`.`id` = `LogicalInterface_IPInterface`.`id`))) join `networkinterface` `LogicalInterface_NetworkInterface` on((`LogicalInterface`.`id` = `LogicalInterface_NetworkInterface`.`id`))) where (0 <> coalesce((`VirtualMachine_virtualmachine_id_VirtualDevice`.`finalclass` = 'VirtualMachine'),1))
```

