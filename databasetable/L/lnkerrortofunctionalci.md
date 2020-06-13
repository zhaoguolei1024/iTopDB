lnkerrortofunctionalci

关联 已知问题/功能配置项 (lnkErrorToFunctionalCI) - 已知问题和功能配置项之间的关联



| 列              | 类型                   | 注释     |
| :-------------- | ---------------------- | -------- |
| link_id         | int *自动增量*         | 自增ID   |
| functionalci_id | int *NULL* [**0**]     | 配置项   |
| error_id        | int *NULL* [**0**]     | 已知问题 |
| dummy           | varchar(255) *NULL* [] |          |

### 索引

| PRIMARY | *link_id*         |
| :------ | ----------------- |
| INDEX   | *functionalci_id* |
| INDEX   | *error_id*        |