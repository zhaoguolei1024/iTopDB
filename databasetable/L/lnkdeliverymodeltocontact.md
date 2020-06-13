lnkdeliverymodeltocontact

关联 交付模式/联系人 (lnkDeliveryModelToContact)



| 列               | 类型               | 注释     |
| :--------------- | ------------------ | -------- |
| id               | int *自动增量*     | 自增ID   |
| deliverymodel_id | int *NULL* [**0**] | 交付模式 |
| contact_id       | int *NULL* [**0**] | 联系人   |
| role_id          | int *NULL* [**0**] | 角色     |

### 索引

| PRIMARY | *id*               |
| :------ | ------------------ |
| INDEX   | *deliverymodel_id* |
| INDEX   | *contact_id*       |
| INDEX   | *role_id*          |