| 列                       | 类型                   | 注释 |
| :----------------------- | ---------------------- | ---- |
| id                       | int [**0**]            |      |
| vlan_tag                 | varchar(255) *NULL* [] |      |
| description              | text *NULL*            |      |
| org_id                   | int *NULL* [**0**]     |      |
| org_name                 | varchar(255) *NULL* [] |      |
| friendlyname             | varchar(255) *NULL*    |      |
| org_id_friendlyname      | varchar(255) *NULL*    |      |
| org_id_obsolescence_flag | int [**0**]            |      |

```
select distinct `VLAN`.`id` AS `id`,`VLAN`.`vlan_tag` AS `vlan_tag`,`VLAN`.`description` AS `description`,`VLAN`.`org_id` AS `org_id`,`Organization_org_id`.`name` AS `org_name`,cast(concat(coalesce(`VLAN`.`vlan_tag`,'')) as char charset utf8mb4) AS `friendlyname`,cast(concat(coalesce(`Organization_org_id`.`name`,'')) as char charset utf8mb4) AS `org_id_friendlyname`,coalesce((`Organization_org_id`.`status` = 'inactive'),0) AS `org_id_obsolescence_flag` from (`vlan` `VLAN` join `organization` `Organization_org_id` on((`VLAN`.`org_id` = `Organization_org_id`.`id`))) where (0 <> 1)
```

