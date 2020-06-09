|              |                                    |      |
| :----------- | ---------------------------------- | ---- |
| 列           | 类型                               | 注释 |
| id           | int [**0**]                        |      |
| name         | varchar(255) *NULL* []             |      |
| finalclass   | varchar(255) *NULL* [**Typology**] |      |
| friendlyname | varchar(255) *NULL*                |      |

```
select distinct `Brand_Typology`.`id` AS `id`,`Brand_Typology`.`name` AS `name`,`Brand_Typology`.`finalclass` AS `finalclass`,cast(concat(coalesce(`Brand_Typology`.`name`,'')) as char charset utf8mb4) AS `friendlyname` from `typology` `Brand_Typology` where (0 <> coalesce((`Brand_Typology`.`finalclass` = 'Brand'),1))
```

