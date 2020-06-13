priv_app_preferences

用户资料 (appUserPreferences)



| 列          | 类型               | 注释   |
| :---------- | ------------------ | ------ |
| id          | int *自动增量*     | 自增ID |
| userid      | int *NULL* [**0**] | 用户   |
| preferences | longtext *NULL*    | 首选项 |

### 索引

| PRIMARY | *id*     |
| :------ | -------- |
| INDEX   | *userid* |