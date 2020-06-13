ticket_request

用户需求 (UserRequest)

工单 (Ticket) >> UserRequest



| 列                         | 类型                                                         | 注释                                                         |
| :------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| id                         | int *自动增量*                                               | 自增ID                                                       |
| status                     | enum('approved','assigned','closed','escalated_tto','escalated_ttr','new','pending','rejected','resolved','waiting_for_approval') *NULL* [**new**] | 状态，已批准 (approved), 已分配 (assigned), 已关闭 (closed), 已升级响应时间 (escalated_tto), 已升级解决时间 (escalated_ttr), 新建 (new), 待定 (pending), 已驳回 (rejected), 已解决 (resolved), 等待批准 (waiting_for_approval) |
| request_type               | enum('service_request') *NULL* [**service_request**]         | 需求类型，服务需求 (service_request)                         |
| impact                     | enum('1','2','3') *NULL* [**1**]                             | 影响范围，部门 (1), 服务 (2), 个体 (3)                       |
| priority                   | enum('1','2','3','4') *NULL* [**4**]                         | 优先级，非常高 (1), 高 (2), 中 (3), 低 (4)                   |
| urgency                    | enum('1','2','3','4') *NULL* [**4**]                         | 紧急度，非常高 (1), 高 (2), 中 (3), 低 (4)                   |
| origin                     | enum('mail','phone','portal') *NULL* [**phone**]             | 来自，邮件 (mail), 电话 (phone), iTop (portal)               |
| approver_id                | int *NULL* [**0**]                                           | 批准人ID                                                     |
| service_id                 | int *NULL* [**0**]                                           | 服务ID                                                       |
| servicesubcategory_id      | int *NULL* [**0**]                                           | 子服务ID                                                     |
| escalation_flag            | enum('no','yes') *NULL* [**no**]                             | 是否升级，否 (no), 是 (yes)                                  |
| escalation_reason          | varchar(255) *NULL* []                                       | 升级原因                                                     |
| assignment_date            | datetime *NULL*                                              | 分配日期                                                     |
| resolution_date            | datetime *NULL*                                              | 解决日期                                                     |
| last_pending_date          | datetime *NULL*                                              | 最后更新                                                     |
| cumulatedpending_timespent | int unsigned *NULL*                                          | 累计待处理时间                                               |
| cumulatedpending_started   | datetime *NULL*                                              | 累计挂起                                                     |
| cumulatedpending_laststart | datetime *NULL*                                              | 累计挂起时间                                                 |
| cumulatedpending_stopped   | datetime *NULL*                                              | 已停止累积挂起                                               |
| tto_timespent              | int unsigned *NULL*                                          |                                                              |
| tto_started                | datetime *NULL*                                              |                                                              |
| tto_laststart              | datetime *NULL*                                              |                                                              |
| tto_stopped                | datetime *NULL*                                              |                                                              |
| tto_75_deadline            | datetime *NULL*                                              |                                                              |
| tto_75_passed              | tinyint unsigned *NULL*                                      |                                                              |
| tto_75_triggered           | tinyint(1) *NULL*                                            |                                                              |
| tto_75_overrun             | int unsigned *NULL*                                          |                                                              |
| tto_100_deadline           | datetime *NULL*                                              |                                                              |
| tto_100_passed             | tinyint unsigned *NULL*                                      |                                                              |
| tto_100_triggered          | tinyint(1) *NULL*                                            |                                                              |
| tto_100_overrun            | int unsigned *NULL*                                          |                                                              |
| ttr_timespent              | int unsigned *NULL*                                          |                                                              |
| ttr_started                | datetime *NULL*                                              |                                                              |
| ttr_laststart              | datetime *NULL*                                              |                                                              |
| ttr_stopped                | datetime *NULL*                                              |                                                              |
| ttr_75_deadline            | datetime *NULL*                                              |                                                              |
| ttr_75_passed              | tinyint unsigned *NULL*                                      |                                                              |
| ttr_75_triggered           | tinyint(1) *NULL*                                            |                                                              |
| ttr_75_overrun             | int unsigned *NULL*                                          |                                                              |
| ttr_100_deadline           | datetime *NULL*                                              |                                                              |
| ttr_100_passed             | tinyint unsigned *NULL*                                      |                                                              |
| ttr_100_triggered          | tinyint(1) *NULL*                                            |                                                              |
| ttr_100_overrun            | int unsigned *NULL*                                          |                                                              |
| time_spent                 | int unsigned *NULL*                                          | 耗时                                                         |
| resolution_code            | enum('assistance','bug fixed','hardware repair','other','software patch','system update','training') *NULL* [**assistance**] | 解决代码，帮助 (assistance), bug修复 (bug fixed), 硬件维修 (hardware repair), 其他 (other), 软件补丁 (software patch), 系统更新 (system update), 培训 (training) |
| solution                   | text *NULL*                                                  | 解决方案                                                     |
| pending_reason             | text *NULL*                                                  | 待定原因                                                     |
| parent_request_id          | int *NULL* [**0**]                                           | 父级需求                                                     |
| parent_incident_id         | int *NULL* [**0**]                                           | 父级事件                                                     |
| parent_problem_id          | int *NULL* [**0**]                                           | 父级问题                                                     |
| parent_change_id           | int *NULL* [**0**]                                           | 父级变更                                                     |
| public_log                 | longtext *NULL*                                              | 评论                                                         |
| public_log_index           | blob *NULL*                                                  | 评论顺序                                                     |
| user_satisfaction          | enum('1','2','3','4') *NULL* [**1**]                         | 用户满意度，非常满意 (1), 基本满意 (2), 不满意 (3), 非常不满意 (4) |
| user_commment              | text *NULL*                                                  | 用户留言                                                     |

### 索引

| PRIMARY | *id*                    |
| :------ | ----------------------- |
| INDEX   | *approver_id*           |
| INDEX   | *service_id*            |
| INDEX   | *servicesubcategory_id* |
| INDEX   | *parent_request_id*     |
| INDEX   | *parent_incident_id*    |
| INDEX   | *parent_problem_id*     |
| INDEX   | *parent_change_id*      |