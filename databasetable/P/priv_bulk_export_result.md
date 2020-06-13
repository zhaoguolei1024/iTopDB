

Bulk Export Result

批量导出结果



| 列              | 类型                      | 注释         |
| :-------------- | ------------------------- | ------------ |
| id              | int *自动增量*            | 自增ID       |
| created         | datetime *NULL*           | 创建时间     |
| user_id         | int *NULL* [**0**]        | 账户         |
| chunk_size      | int *NULL* [**0**]        | 块大小       |
| format          | varchar(255) *NULL* []    | 格式         |
| temp_file_path  | varchar(255) *NULL* []    | 临时文件路径 |
| search          | longtext *NULL*           | 搜索         |
| status_info     | longtext *NULL*           | 状态信息     |
| localize_output | tinyint(1) *NULL* [**1**] | 本地化输出   |

### 索引

| PRIMARY | *id*      |
| :------ | --------- |
| INDEX   | *created* |