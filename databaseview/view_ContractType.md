| 列           | 类型                               | 注释 |
| :----------- | ---------------------------------- | ---- |
| id           | int [**0**]                        |      |
| name         | varchar(255) *NULL* []             |      |
| finalclass   | varchar(255) *NULL* [**Typology**] |      |
| friendlyname | varchar(255) *NULL*                |      |

```
select distinct `ContractType_Typology`.`id` AS `id`,`ContractType_Typology`.`name` AS `name`,`ContractType_Typology`.`finalclass` AS `finalclass`,cast(concat(coalesce(`ContractType_Typology`.`name`,'')) as char charset utf8mb4) AS `friendlyname` from `typology` `ContractType_Typology` where (0 <> coalesce((`ContractType_Typology`.`finalclass` = 'ContractType'),1))
```

