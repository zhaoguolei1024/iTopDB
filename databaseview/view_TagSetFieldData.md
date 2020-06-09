| 列           | 类型                                      | 注释 |
| :----------- | ----------------------------------------- | ---- |
| id           | int [**0**]                               |      |
| code         | varchar(255) *NULL* []                    |      |
| label        | varchar(255) *NULL* []                    |      |
| description  | longtext *NULL*                           |      |
| obj_class    | varchar(255) *NULL* []                    |      |
| obj_attcode  | varchar(255) *NULL* []                    |      |
| finalclass   | varchar(255) *NULL* [**TagSetFieldData**] |      |
| friendlyname | varchar(255) *NULL*                       |      |

```
select distinct `TagSetFieldData`.`id` AS `id`,`TagSetFieldData`.`code` AS `code`,`TagSetFieldData`.`label` AS `label`,`TagSetFieldData`.`description` AS `description`,`TagSetFieldData`.`obj_class` AS `obj_class`,`TagSetFieldData`.`obj_attcode` AS `obj_attcode`,`TagSetFieldData`.`finalclass` AS `finalclass`,cast(concat(coalesce(`TagSetFieldData`.`label`,'')) as char charset utf8mb4) AS `friendlyname` from `priv_tagfielddata` `TagSetFieldData` where (0 <> 1)
```

