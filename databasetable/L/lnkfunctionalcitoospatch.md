lnkfunctionalcitoospatch



链接 功能项 / 操作系统补丁 (lnkFunctionalCIToOSPatch)



| 列              | 类型               | 注释         |
| :-------------- | ------------------ | ------------ |
| id              | int *自动增量*     | 自增ID       |
| ospatch_id      | int *NULL* [**0**] | 操作系统补丁 |
| functionalci_id | int *NULL* [**0**] | 功能项       |

### 索引

| PRIMARY | *id*              |
| :------ | ----------------- |
| INDEX   | *ospatch_id*      |
| INDEX   | *functionalci_id* |