| 列           | 类型                               | 注释 |
| :----------- | ---------------------------------- | ---- |
| id           | int [**0**]                        |      |
| name         | varchar(255) *NULL* []             |      |
| finalclass   | varchar(255) *NULL* [**Typology**] |      |
| friendlyname | varchar(255) *NULL*                |      |

```
select distinct `DocumentType_Typology`.`id` AS `id`,`DocumentType_Typology`.`name` AS `name`,`DocumentType_Typology`.`finalclass` AS `finalclass`,cast(concat(coalesce(`DocumentType_Typology`.`name`,'')) as char charset utf8mb4) AS `friendlyname` from `typology` `DocumentType_Typology` where (0 <> coalesce((`DocumentType_Typology`.`finalclass` = 'DocumentType'),1))
```

