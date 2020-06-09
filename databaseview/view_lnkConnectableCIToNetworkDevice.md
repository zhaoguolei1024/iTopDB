| 列                                 | 类型                                            | 注释 |
| :--------------------------------- | ----------------------------------------------- | ---- |
| id                                 | int [**0**]                                     |      |
| networkdevice_id                   | int *NULL* [**0**]                              |      |
| networkdevice_name                 | varchar(255) *NULL* []                          |      |
| connectableci_id                   | int *NULL* [**0**]                              |      |
| connectableci_name                 | varchar(255) *NULL* []                          |      |
| network_port                       | varchar(255) *NULL* []                          |      |
| device_port                        | varchar(255) *NULL* []                          |      |
| connection_type                    | enum('downlink','uplink') *NULL* [**downlink**] |      |
| friendlyname                       | varchar(23) *NULL*                              |      |
| networkdevice_id_friendlyname      | varchar(255) *NULL*                             |      |
| networkdevice_id_obsolescence_flag | int [**0**]                                     |      |
| connectableci_id_friendlyname      | varchar(255) *NULL*                             |      |
| connectableci_id_finalclass_recall | varchar(255) *NULL* [**FunctionalCI**]          |      |
| connectableci_id_obsolescence_flag | int [**0**]                                     |      |

```
select distinct `lnkConnectableCIToNetworkDevice`.`id` AS `id`,`lnkConnectableCIToNetworkDevice`.`networkdevice_id` AS `networkdevice_id`,`NetworkDevice_networkdevice_id_FunctionalCI`.`name` AS `networkdevice_name`,`lnkConnectableCIToNetworkDevice`.`connectableci_id` AS `connectableci_id`,`ConnectableCI_connectableci_id_FunctionalCI`.`name` AS `connectableci_name`,`lnkConnectableCIToNetworkDevice`.`network_port` AS `network_port`,`lnkConnectableCIToNetworkDevice`.`device_port` AS `device_port`,`lnkConnectableCIToNetworkDevice`.`type` AS `connection_type`,cast(concat(coalesce(`lnkConnectableCIToNetworkDevice`.`networkdevice_id`,''),coalesce(' ',''),coalesce(`lnkConnectableCIToNetworkDevice`.`connectableci_id`,'')) as char charset utf8mb4) AS `friendlyname`,cast(concat(coalesce(`NetworkDevice_networkdevice_id_FunctionalCI`.`name`,'')) as char charset utf8mb4) AS `networkdevice_id_friendlyname`,coalesce((`NetworkDevice_networkdevice_id_PhysicalDevice`.`status` = 'obsolete'),0) AS `networkdevice_id_obsolescence_flag`,cast(concat(coalesce(`ConnectableCI_connectableci_id_FunctionalCI`.`name`,'')) as char charset utf8mb4) AS `connectableci_id_friendlyname`,`ConnectableCI_connectableci_id_FunctionalCI`.`finalclass` AS `connectableci_id_finalclass_recall`,coalesce((`ConnectableCI_connectableci_id_PhysicalDevice`.`status` = 'obsolete'),0) AS `connectableci_id_obsolescence_flag` from ((`lnkconnectablecitonetworkdevice` `lnkConnectableCIToNetworkDevice` join (`physicaldevice` `NetworkDevice_networkdevice_id_PhysicalDevice` join `functionalci` `NetworkDevice_networkdevice_id_FunctionalCI` on((`NetworkDevice_networkdevice_id_PhysicalDevice`.`id` = `NetworkDevice_networkdevice_id_FunctionalCI`.`id`))) on((`lnkConnectableCIToNetworkDevice`.`networkdevice_id` = `NetworkDevice_networkdevice_id_PhysicalDevice`.`id`))) join (`physicaldevice` `ConnectableCI_connectableci_id_PhysicalDevice` join `functionalci` `ConnectableCI_connectableci_id_FunctionalCI` on((`ConnectableCI_connectableci_id_PhysicalDevice`.`id` = `ConnectableCI_connectableci_id_FunctionalCI`.`id`))) on((`lnkConnectableCIToNetworkDevice`.`connectableci_id` = `ConnectableCI_connectableci_id_PhysicalDevice`.`id`))) where ((0 <> coalesce((`NetworkDevice_networkdevice_id_PhysicalDevice`.`finalclass` = 'NetworkDevice'),1)) and (0 <> coalesce((`ConnectableCI_connectableci_id_PhysicalDevice`.`finalclass` in ('DatacenterDevice','NetworkDevice','Server','PC','Printer','StorageSystem','SANSwitch','TapeLibrary','NAS','ConnectableCI')),1)))
```

