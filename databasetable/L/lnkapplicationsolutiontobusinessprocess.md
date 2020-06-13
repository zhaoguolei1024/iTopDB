lnkapplicationsolutiontobusinessprocess

链接 应用方案 / 业务流程 (lnkApplicationSolutionToBusinessProcess)



| 列                     | 类型               | 注释     |
| :--------------------- | ------------------ | -------- |
| id                     | int *自动增量*     | 自增ID   |
| businessprocess_id     | int *NULL* [**0**] | 业务流程 |
| applicationsolution_id | int *NULL* [**0**] | 应用方案 |

### 索引

| PRIMARY | *id*                     |
| :------ | ------------------------ |
| INDEX   | *businessprocess_id*     |
| INDEX   | *applicationsolution_id* |