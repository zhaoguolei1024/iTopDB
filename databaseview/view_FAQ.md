| 列                       | 类型                   | 注释 |
| :----------------------- | ---------------------- | ---- |
| id                       | int [**0**]            |      |
| title                    | varchar(255) *NULL* [] |      |
| summary                  | text *NULL*            |      |
| description              | longtext *NULL*        |      |
| category_id              | int *NULL* [**0**]     |      |
| category_name            | varchar(255) *NULL* [] |      |
| error_code               | varchar(255) *NULL* [] |      |
| key_words                | varchar(255) *NULL* [] |      |
| domains                  | varchar(255) *NULL* [] |      |
| friendlyname             | varchar(255) *NULL*    |      |
| category_id_friendlyname | varchar(255) *NULL*    |      |

```
SELECT DISTINCT
	`FAQ`.`id` AS `id`,
	`FAQ`.`title` AS `title`,
	`FAQ`.`summary` AS `summary`,
	`FAQ`.`description` AS `description`,
	`FAQ`.`category_id` AS `category_id`,
	`FAQCategory_category_id`.`nam` AS `category_name`,
	`FAQ`.`error_code` AS `error_code`,
	`FAQ`.`key_words` AS `key_words`,
	`FAQ`.`domains` AS `domains`,
	cast( concat( COALESCE ( `FAQ`.`title`, '' )) AS CHAR charset utf8mb4 ) AS `friendlyname`,
	cast( concat( COALESCE ( `FAQCategory_category_id`.`nam`, '' )) AS CHAR charset utf8mb4 ) AS `category_id_friendlyname` 
FROM
	(
		`faq` `FAQ`
		JOIN `faqcategory` `FAQCategory_category_id` ON ((
				`FAQ`.`category_id` = `FAQCategory_category_id`.`id` 
			))) 
WHERE
	(
	0 <> 1)
```

