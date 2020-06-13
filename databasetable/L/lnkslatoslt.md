lnkslatoslt

关联 SLA/SLT (lnkSLAToSLT)



| 列     | 类型               | 注释   |
| :----- | ------------------ | ------ |
| id     | int *自动增量*     | 自增ID |
| sla_id | int *NULL* [**0**] | SLA    |
| slt_id | int *NULL* [**0**] | SLT    |

### 索引

| PRIMARY | *id*     |
| :------ | -------- |
| INDEX   | *sla_id* |
| INDEX   | *slt_id* |