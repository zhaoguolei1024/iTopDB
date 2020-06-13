priv_changeop_attachment_added

CMDBChangeOpAttachmentAdded (CMDBChangeOpAttachmentAdded)

变更操作 (CMDBChangeOp) >> CMDBChangeOpAttachmentAdded

| 列            | 类型                   | 注释     |
| :------------ | ---------------------- | -------- |
| id            | int                    | 自增ID   |
| attachment_id | int *NULL* [**0**]     | 附件ID   |
| filename      | varchar(255) *NULL* [] | 文件名称 |

### 索引

| PRIMARY | *id*            |
| :------ | --------------- |
| INDEX   | *attachment_id* |