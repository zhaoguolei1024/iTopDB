lnkcontacttoticket



关联 联系人/工单 (lnkContactToTicket)



| 列          | 类型                                                         | 注释                                                         |
| :---------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| id          | int *自动增量*                                               | 自增ID                                                       |
| ticket_id   | int *NULL* [**0**]                                           | 工单                                                         |
| contact_id  | int *NULL* [**0**]                                           | 联系人                                                       |
| role        | varchar(255) *NULL* []                                       | 角色 (文本)                                                  |
| impact_code | enum('computed','do_not_notify','manual') *NULL* [**manual**] | 角色，自动添加 (computed), 不通知 (do_not_notify), 手动添加 (manual) |

### 索引

| PRIMARY | *id*         |
| :------ | ------------ |
| INDEX   | *ticket_id*  |
| INDEX   | *contact_id* |