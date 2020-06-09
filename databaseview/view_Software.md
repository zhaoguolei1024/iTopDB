| 列           | 类型                                                         | 注释 |
| :----------- | ------------------------------------------------------------ | ---- |
| id           | int [**0**]                                                  |      |
| name         | varchar(255) *NULL* []                                       |      |
| vendor       | varchar(255) *NULL* []                                       |      |
| version      | varchar(255) *NULL* []                                       |      |
| type         | enum('DBServer','Middleware','OtherSoftware','PCSoftware','WebServer') *NULL* |      |
| friendlyname | varchar(511) *NULL*                                          |      |

```
select distinct `Software`.`id` AS `id`,`Software`.`name` AS `name`,`Software`.`vendor` AS `vendor`,`Software`.`version` AS `version`,`Software`.`type` AS `type`,cast(concat(coalesce(`Software`.`name`,''),coalesce(' ',''),coalesce(`Software`.`version`,'')) as char charset utf8mb4) AS `friendlyname` from `software` `Software` where (0 <> 1)
```

