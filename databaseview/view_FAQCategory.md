| 列           | 类型                   | 注释 |
| :----------- | ---------------------- | ---- |
| id           | int [**0**]            |      |
| name         | varchar(255) *NULL* [] |      |
| friendlyname | varchar(255) *NULL*    |      |

```
select distinct `FAQCategory`.`id` AS `id`,`FAQCategory`.`nam` AS `name`,cast(concat(coalesce(`FAQCategory`.`nam`,'')) as char charset utf8mb4) AS `friendlyname` from `faqcategory` `FAQCategory` where (0 <> 1)
```

