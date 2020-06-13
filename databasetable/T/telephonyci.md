telephonyci

Telephony CI (TelephonyCI)

功能配置项 (FunctionalCI) >> 物理设备 (PhysicalDevice) >> TelephonyCI



| 列          | 类型                                  | 注释     |
| :---------- | ------------------------------------- | -------- |
| id          | int *自动增量*                        | 自增ID   |
| phonenumber | varchar(255) *NULL* []                | 电话号码 |
| finalclass  | varchar(255) *NULL* [**TelephonyCI**] | 分类     |

### 索引

| PRIMARY | *id*             |
| :------ | ---------------- |
| INDEX   | *finalclass*(95) |