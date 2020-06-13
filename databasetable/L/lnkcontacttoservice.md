lnkcontacttoservice



关联 联系人/服务 (lnkContactToService)



| 列         | 类型               | 注释   |
| :--------- | ------------------ | ------ |
| id         | int *自动增量*     | 自增ID |
| service_id | int *NULL* [**0**] | 服务   |
| contact_id | int *NULL* [**0**] | 联系人 |

### 索引

| PRIMARY | *id*         |
| :------ | ------------ |
| INDEX   | *service_id* |
| INDEX   | *contact_id* |