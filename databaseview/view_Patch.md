| 列           | 类型                            | 注释 |
| :----------- | ------------------------------- | ---- |
| id           | int [**0**]                     |      |
| name         | varchar(255) *NULL* []          |      |
| description  | text *NULL*                     |      |
| finalclass   | varchar(255) *NULL* [**Patch**] |      |
| friendlyname | varchar(255) *NULL*             |      |

```
select distinct `Patch`.`id` AS `id`,`Patch`.`name` AS `name`,`Patch`.`description` AS `description`,`Patch`.`finalclass` AS `finalclass`,cast(concat(coalesce(`Patch`.`name`,'')) as char charset utf8mb4) AS `friendlyname` from `patch` `Patch` where (0 <> 1)
```

