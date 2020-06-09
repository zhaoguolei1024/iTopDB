| 列           | 类型                               | 注释 |
| :----------- | ---------------------------------- | ---- |
| id           | int [**0**]                        |      |
| name         | varchar(255) *NULL* []             |      |
| finalclass   | varchar(255) *NULL* [**Typology**] |      |
| friendlyname | varchar(255) *NULL*                |      |

```
select distinct `OSFamily_Typology`.`id` AS `id`,`OSFamily_Typology`.`name` AS `name`,`OSFamily_Typology`.`finalclass` AS `finalclass`,cast(concat(coalesce(`OSFamily_Typology`.`name`,'')) as char charset utf8mb4) AS `friendlyname` from `typology` `OSFamily_Typology` where (0 <> coalesce((`OSFamily_Typology`.`finalclass` = 'OSFamily'),1))
```

