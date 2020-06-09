|              |                                    |      |
| :----------- | ---------------------------------- | ---- |
| 列           | 类型                               | 注释 |
| id           | int [**0**]                        |      |
| name         | varchar(255) *NULL* []             |      |
| finalclass   | varchar(255) *NULL* [**Typology**] |      |
| friendlyname | varchar(255) *NULL*                |      |

```
select distinct `ContactType_Typology`.`id` AS `id`,`ContactType_Typology`.`name` AS `name`,`ContactType_Typology`.`finalclass` AS `finalclass`,cast(concat(coalesce(`ContactType_Typology`.`name`,'')) as char charset utf8mb4) AS `friendlyname` from `typology` `ContactType_Typology` where (0 <> coalesce((`ContactType_Typology`.`finalclass` = 'ContactType'),1))
```

