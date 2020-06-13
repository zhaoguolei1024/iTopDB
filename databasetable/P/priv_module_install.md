priv_module_install

ModuleInstallation (ModuleInstallation)

模块安装

| 列        | 类型                   | 注释     |
| :-------- | ---------------------- | -------- |
| id        | int *自动增量*         | 自增ID   |
| name      | varchar(255) *NULL* [] | 名称     |
| version   | varchar(255) *NULL* [] | 版本     |
| installed | datetime *NULL*        | 安装日期 |
| comment   | text *NULL*            | 备注     |
| parent_id | int *NULL* [**0**]     | 父ID     |

### 索引

| PRIMARY | *id*        |
| :------ | ----------- |
| INDEX   | *parent_id* |