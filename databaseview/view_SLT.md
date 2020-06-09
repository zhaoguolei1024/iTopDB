| 列           | 类型                                      | 注释 |
| :----------- | ----------------------------------------- | ---- |
| id           | int [**0**]                               |      |
| name         | varchar(255) *NULL* []                    |      |
| priority     | enum('1','2','3','4') *NULL*              |      |
| request_type | enum('incident','service_request') *NULL* |      |
| metric       | enum('tto','ttr') *NULL*                  |      |
| value        | int *NULL*                                |      |
| unit         | enum('hours','minutes') *NULL*            |      |
| friendlyname | varchar(255) *NULL*                       |      |

```
select distinct `SLT`.`id` AS `id`,`SLT`.`name` AS `name`,`SLT`.`priority` AS `priority`,`SLT`.`request_type` AS `request_type`,`SLT`.`metric` AS `metric`,`SLT`.`value` AS `value`,`SLT`.`unit` AS `unit`,cast(concat(coalesce(`SLT`.`name`,'')) as char charset utf8mb4) AS `friendlyname` from `slt` `SLT` where (0 <> 1)
```

