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
select distinct `TagSetFieldDataFor_FAQ__domains_TagSetFieldData`.`id` AS `id`,`TagSetFieldDataFor_FAQ__domains_TagSetFieldData`.`code` AS `code`,`TagSetFieldDataFor_FAQ__domains_TagSetFieldData`.`label` AS `label`,`TagSetFieldDataFor_FAQ__domains_TagSetFieldData`.`description` AS `description`,`TagSetFieldDataFor_FAQ__domains_TagSetFieldData`.`obj_class` AS `obj_class`,`TagSetFieldDataFor_FAQ__domains_TagSetFieldData`.`obj_attcode` AS `obj_attcode`,`TagSetFieldDataFor_FAQ__domains_TagSetFieldData`.`finalclass` AS `finalclass`,cast(concat(coalesce(`TagSetFieldDataFor_FAQ__domains_TagSetFieldData`.`label`,'')) as char charset utf8mb4) AS `friendlyname` from `priv_tagfielddata` `TagSetFieldDataFor_FAQ__domains_TagSetFieldData` where (0 <> coalesce((`TagSetFieldDataFor_FAQ__domains_TagSetFieldData`.`finalclass` = 'TagSetFieldDataFor_FAQ__domains'),1))
```

