| 列           | 类型                            | 注释 |
| :----------- | ------------------------------- | ---- |
| id           | int *自动增量*                  |      |
| osfamily_id  | int *NULL* [**0**]              |      |
| osversion_id | int *NULL* [**0**]              |      |
| cpu          | varchar(255) *NULL* []          |      |
| ram          | varchar(255) *NULL* []          |      |
| type         | enum('desktop','laptop') *NULL* |      |

### 索引

| PRIMARY | *id*           |
| :------ | -------------- |
| INDEX   | *osfamily_id*  |
| INDEX   | *osversion_id* |