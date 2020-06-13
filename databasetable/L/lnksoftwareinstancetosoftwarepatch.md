lnksoftwareinstancetosoftwarepatch

链接 软件实例 / 软件补丁 (lnkSoftwareInstanceToSoftwarePatch)



| 列                  | 类型               | 注释     |
| :------------------ | ------------------ | -------- |
| id                  | int *自动增量*     | 自增ID   |
| softwarepatch_id    | int *NULL* [**0**] | 软件补丁 |
| softwareinstance_id | int *NULL* [**0**] | 软件实例 |

### 索引

| PRIMARY | *id*                  |
| :------ | --------------------- |
| INDEX   | *softwarepatch_id*    |
| INDEX   | *softwareinstance_id* |