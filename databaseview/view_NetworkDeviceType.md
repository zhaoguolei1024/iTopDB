| 列           | 类型                               | 注释 |
| :----------- | ---------------------------------- | ---- |
| id           | int [**0**]                        |      |
| name         | varchar(255) *NULL* []             |      |
| finalclass   | varchar(255) *NULL* [**Typology**] |      |
| friendlyname | varchar(255) *NULL*                |      |

```
select distinct `NetworkDeviceType_Typology`.`id` AS `id`,`NetworkDeviceType_Typology`.`name` AS `name`,`NetworkDeviceType_Typology`.`finalclass` AS `finalclass`,cast(concat(coalesce(`NetworkDeviceType_Typology`.`name`,'')) as char charset utf8mb4) AS `friendlyname` from `typology` `NetworkDeviceType_Typology` where (0 <> coalesce((`NetworkDeviceType_Typology`.`finalclass` = 'NetworkDeviceType'),1))
```

