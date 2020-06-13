priv_shortcut_oql

搜索结果的快捷方式 (ShortcutOQL)

快捷方式 (Shortcut) >> ShortcutOQL



| 列              | 类型                                    | 注释                                       |
| :-------------- | --------------------------------------- | ------------------------------------------ |
| id              | int *自动增量*                          | 自增ID                                     |
| oql             | text *NULL*                             | 查询                                       |
| auto_reload     | enum('custom','none') *NULL* [**none**] | 自动刷新，自定义频率 (custom), 禁用 (none) |
| auto_reload_sec | int *NULL* [**60**]                     | 自动刷新间隔(秒)                           |

### 索引

| PRIMARY | *id* |
| :------ | ---- |
|         |      |