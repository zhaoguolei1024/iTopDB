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
SELECT DISTINCT
	`TagSetFieldData`.`id` AS `id`,
	`TagSetFieldData`.`code` AS `code`,
	`TagSetFieldData`.`label` AS `label`,
	`TagSetFieldData`.`description` AS `description`,
	`TagSetFieldData`.`obj_class` AS `obj_class`,
	`TagSetFieldData`.`obj_attcode` AS `obj_attcode`,
	`TagSetFieldData`.`finalclass` AS `finalclass`,
	cast( concat( COALESCE ( `TagSetFieldData`.`label`, '' )) AS CHAR charset utf8mb4 ) AS `friendlyname` 
FROM
	`priv_tagfielddata` `TagSetFieldData` 
WHERE
	(
	0 <> 1)
```

