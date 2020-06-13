lnkfunctionalcitoticket

关联 功能配置项/工单 (lnkFunctionalCIToTicket)



| 列              | 类型                                                         | 注释                                                         |
| :-------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| id              | int *自动增量*                                               | 自增ID                                                       |
| ticket_id       | int *NULL* [**0**]                                           | 工单                                                         |
| functionalci_id | int *NULL* [**0**]                                           | 配置项                                                       |
| impact          | varchar(255) *NULL* []                                       | 影响 (文本)                                                  |
| impact_code     | enum('computed','manual','not_impacted') *NULL* [**manual**] | 影响，自动添加 (computed), 手动添加 (manual), 不通知 (not_impacted) |

### 索引

| PRIMARY | *id*              |
| :------ | ----------------- |
| INDEX   | *ticket_id*       |
| INDEX   | *functionalci_id* |