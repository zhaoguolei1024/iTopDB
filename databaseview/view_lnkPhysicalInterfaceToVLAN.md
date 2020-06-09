| 列                                            | 类型                   | 注释 |
| :-------------------------------------------- | ---------------------- | ---- |
| id                                            | int [**0**]            |      |
| physicalinterface_id                          | int *NULL* [**0**]     |      |
| physicalinterface_name                        | varchar(255) *NULL* [] |      |
| physicalinterface_device_id                   | int *NULL* [**0**]     |      |
| physicalinterface_device_name                 | varchar(255) *NULL* [] |      |
| vlan_id                                       | int *NULL* [**0**]     |      |
| vlan_tag                                      | varchar(255) *NULL* [] |      |
| friendlyname                                  | varchar(23) *NULL*     |      |
| physicalinterface_id_friendlyname             | varchar(511) *NULL*    |      |
| physicalinterface_id_obsolescence_flag        | int [**0**]            |      |
| physicalinterface_device_id_friendlyname      | varchar(255) *NULL*    |      |
| physicalinterface_device_id_obsolescence_flag | int [**0**]            |      |
| vlan_id_friendlyname                          | varchar(255) *NULL*    |      |

```
select distinct `lnkPhysicalInterfaceToVLAN`.`id` AS `id`,`lnkPhysicalInterfaceToVLAN`.`physicalinterface_id` AS `physicalinterface_id`,`PhysicalInterface_physicalinterface_id_NetworkInterface`.`name` AS `physicalinterface_name`,`PhysicalInterface_physicalinterface_id`.`connectableci_id` AS `physicalinterface_device_id`,`ConnectableCI_connectableci_id_FunctionalCI`.`name` AS `physicalinterface_device_name`,`lnkPhysicalInterfaceToVLAN`.`vlan_id` AS `vlan_id`,`VLAN_vlan_id`.`vlan_tag` AS `vlan_tag`,cast(concat(coalesce(`lnkPhysicalInterfaceToVLAN`.`physicalinterface_id`,''),coalesce(' ',''),coalesce(`lnkPhysicalInterfaceToVLAN`.`vlan_id`,'')) as char charset utf8mb4) AS `friendlyname`,cast(concat(coalesce(`PhysicalInterface_physicalinterface_id_NetworkInterface`.`name`,''),coalesce(' ',''),coalesce(`ConnectableCI_connectableci_id_FunctionalCI`.`name`,'')) as char charset utf8mb4) AS `physicalinterface_id_friendlyname`,coalesce(coalesce((`ConnectableCI_connectableci_id_PhysicalDevice`.`status` = 'obsolete'),0),0) AS `physicalinterface_id_obsolescence_flag`,cast(concat(coalesce(`ConnectableCI_connectableci_id_FunctionalCI`.`name`,'')) as char charset utf8mb4) AS `physicalinterface_device_id_friendlyname`,coalesce((`ConnectableCI_connectableci_id_PhysicalDevice`.`status` = 'obsolete'),0) AS `physicalinterface_device_id_obsolescence_flag`,cast(concat(coalesce(`VLAN_vlan_id`.`vlan_tag`,'')) as char charset utf8mb4) AS `vlan_id_friendlyname` from ((`lnkphysicalinterfacetovlan` `lnkPhysicalInterfaceToVLAN` join ((`physicalinterface` `PhysicalInterface_physicalinterface_id` join (`physicaldevice` `ConnectableCI_connectableci_id_PhysicalDevice` join `functionalci` `ConnectableCI_connectableci_id_FunctionalCI` on((`ConnectableCI_connectableci_id_PhysicalDevice`.`id` = `ConnectableCI_connectableci_id_FunctionalCI`.`id`))) on((`PhysicalInterface_physicalinterface_id`.`connectableci_id` = `ConnectableCI_connectableci_id_PhysicalDevice`.`id`))) join `networkinterface` `PhysicalInterface_physicalinterface_id_NetworkInterface` on((`PhysicalInterface_physicalinterface_id`.`id` = `PhysicalInterface_physicalinterface_id_NetworkInterface`.`id`))) on((`lnkPhysicalInterfaceToVLAN`.`physicalinterface_id` = `PhysicalInterface_physicalinterface_id`.`id`))) join `vlan` `VLAN_vlan_id` on((`lnkPhysicalInterfaceToVLAN`.`vlan_id` = `VLAN_vlan_id`.`id`))) where (0 <> coalesce((`ConnectableCI_connectableci_id_PhysicalDevice`.`finalclass` in ('DatacenterDevice','NetworkDevice','Server','PC','Printer','StorageSystem','SANSwitch','TapeLibrary','NAS','ConnectableCI')),1))
```

