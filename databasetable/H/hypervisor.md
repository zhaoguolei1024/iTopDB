

hypervisor

Hypervisor (Hypervisor)

Hypervisor，又称虚拟机监视器（英语：virtual machine monitor，缩写为 VMM），是用来建立与执行虚拟机器的软件、固件或硬件。

功能配置项 (FunctionalCI) >> 虚拟设备 (VirtualDevice) >> 宿主机 (VirtualHost) >> Hypervisor



| 列        | 类型               | 注释   |
| :-------- | ------------------ | ------ |
| id        | int *自动增量*     | 自增ID |
| farm_id   | int *NULL* [**0**] | 集群   |
| server_id | int *NULL* [**0**] | 物理机 |

### 索引

| PRIMARY | *id*        |
| :------ | ----------- |
| INDEX   | *farm_id*   |
| INDEX   | *server_id* |