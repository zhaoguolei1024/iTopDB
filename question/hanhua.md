##  管理工具--用户管理--角色汉化

汉化效果：

![image-20200609094459568](..\assets\juesehanhua.png)

汉化操作：

1.连接数据库，角色信息描述表：priv_urp_profiles

2.修改该表的描述字段即可



参考数据：

| id   | name                  | description                                                  |
| ---- | --------------------- | ------------------------------------------------------------ |
| 1    | Administrator         | English：Has the rights on everything (bypassing any control) \|\| 简体中文：具有最高的权限，能绕过任何控制。 |
| 2    | Portal user           | English：Has the rights to access to the user portal. People having this profile will not be allowed to access the standard application, they will be automatically redirected to the user portal \|\| 简体中文：门户用户能访问门户首页。不具有其他任何标准应用访问权限的人，将被自动重定向到用户门户首页。 |
| 3    | Configuration Manager | English：Person in charge of the documentation of the managed CIs \|\| 简体中文：配置经理是修改维护CMDB配置项的人。 |
| 4    | Service Desk Agent    | English：Person in charge of creating incident reports \|\| 简体中文：服务台人员是负责事件工单创建和更新的人。现已变更为需求管理标签。 |
| 5    | Support Agent         | English：Person analyzing and solving the current incidents \|\| 简体中文：支持人员是分析和解决当前工单的人。无关备注：一个用户可以有多个角色，并通过角色叠加的方式来实现不同级别的管理权限，系统不支持自定义权限角色，但可以自定义角色权限。 |
| 6    | Problem Manager       | English：Person analyzing and solving the current problems \|\| 简体中文：问题经理是分析和解决当前问题的人。 |
| 7    | Change Implementor    | English：Person executing the changes \|\| 简体中文：变更实施者是执行变更操作的人。 |
| 8    | Change Supervisor     | English：Person responsible for the overall change execution \|\| 简体中文：变更监督者是对变更执行过程整体负责的人。 |
| 9    | Change Approver       | English：Person who could be impacted by some changes \|\| 简体中文：变更审批者是能营销变更审批的人。 |
| 10   | Service Manager       | English：Person responsible for the service delivered to the [internal] customer \|\| 简体中文：服务经理是负责把服务交付给客户（内部和外部）的人。 |
| 11   | Document author       | English：Any person who could contribute to documentation \|\| 简体中文：文档作者是能贡献文档的人。 |
| 12   | Portal power user     | English：Users having this profile will have the rights to see all the tickets for a customer in the portal. Must be used in conjunction with other profiles (e.g. Portal User) \|\| 简体中文：门户高级用户是能够查看某个用户下所有工单的人。它还必须具有其他角色，如门户用户的角色。 |
| 1024 | REST Services User    | English：Only users having this profile are allowed to use the REST Web Services (unless 'secure_rest_services' is set to false in the configuration file) \|\| 简体中文：只有具有此配置文件的用户才允许使用REST Web服务（除非在配置文件中将“secure_rest_services”设置为false）。 |