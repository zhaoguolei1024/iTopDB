| 列              | 类型                      | 注释 |
| :-------------- | ------------------------- | ---- |
| id              | int *自动增量*            |      |
| created         | datetime *NULL*           |      |
| user_id         | int *NULL* [**0**]        |      |
| chunk_size      | int *NULL* [**0**]        |      |
| format          | varchar(255) *NULL* []    |      |
| temp_file_path  | varchar(255) *NULL* []    |      |
| search          | longtext *NULL*           |      |
| status_info     | longtext *NULL*           |      |
| localize_output | tinyint(1) *NULL* [**1**] |      |

### 索引

| PRIMARY | *id*      |
| :------ | --------- |
| INDEX   | *created* |