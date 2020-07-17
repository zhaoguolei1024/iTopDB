# Enhanced global search

- name:

  Enhanced global search

- description:

  Use a faster and more relevant global search with easy-to-filter results

- version:

  1.0.13

- release:

  2020-06-29

- itop-version-min:

  2.5.0

- code:

  combodo-fulltext-search

- state:

  stable

- diffusion:

  Client Store, iTop Hub

This extension replace the standard global search with a faster and more accurate search.

This extension requires Index FullText, so **MySQL 5.6+** or **Mariadb 10.0.5+**

## Features

- Users can improve results accuracy by specifying required, optional and denied words.
- Administrator can fine-tune the results relevance, by changing configuration parameters.
- It uses MySQL fulltext feature to perform the global search.

## Revision History

| Release Date | Version | Comments                                                     |
| ------------ | ------- | ------------------------------------------------------------ |
| 2020-06-29   | 1.0.13  | - Compatibility iTop 2.7 - Fix searches with some reserved characters - Search admin menu |
| 2019-02-04   | 1.0.11  | - Fix broken related link                                    |
| 2019-01-09   | 1.0.10  | - Fix the friendly name limit - Fix Scheduled task - Fix class name in tests - Add Combodo license |
| 2019-01-09   | 1.0.9   | - Fix memory limit - Fix Case log indexation - Fix email search - Limit the friendlyname size to fit in the DB |
| 2018-07-31   | 1.0.8   | - Better indexation - Better search - Support only InnoDB and BOOLEAN mode - Display related objects on search - Display matching fields - Admin page : for re-indexation - Class drill-down - Debug mode |
| 2018-01-19   | 0.0.3   | - Better indexation when updating data - 'populate_search.php' uses the configuration for the type of table to create (MyISAM or InnoDB) - No constraint on MySQL (MyISAM must be used in version before 5.6) |
| 2018-01-09   | 0.0.2   | - Better error management. - No indexation at setup (performance issues). - 'populate_search.php' have to be used to create an InnoDB fulltext index. - MySQL >= 5.6 |
| 2017-12-14   | 0.0.1   | - First version experimental.                                |

## Limitations

- This extension relies on MySQL full-text feature.
- It uses the main database configured for iTop.

## Requirements

- MySQL 5.6 or above
- Mariadb 10.0.5 or above
- iTop 2.5.0 or above

## Installation

Use the [Standard installation process](https://www.itophub.io/wiki/page?id=extensions%3Ainstallation) for this extension.

If the database is big, the index creation can run for a long time. It is possible to populate the full-text index by calling the following page:

```
<itop_url>/env-production/combodo-fulltext-search/populate-search-index.cli.php
```

## Configuration

| Parameter                                | Type    | Description                                                  | Default value                                                |
| ---------------------------------------- | ------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| object_weight_factor                     | array   | Weight factor to apply for a given object name (format: 'classname' ⇒ 'value') the values can vary from 0 to 10 generally (0 means no results for this class). The default is 1 for every class not specified. The modification of this parameter needs a complete re-indexation of the database. | `array(  'Organization' => 2.0,  'Person' => 1.5,  'Location' => 1.2,  'SLT' => 0.8, )` |
| sentence_weight_factor                   | float   | Weight factor for searches with multiple words matching exactly the list of words in that order. | 10.0                                                         |
| mandatory_weight_factor                  | float   | Weight factor for searches with all the words of the search matching at least once. | 2.0                                                          |
| start_with_weight_factor                 | float   | Weight factor for searches with one word matching the beginning. | 0.5                                                          |
| max_interactive_index_update_time_in_sec | integer | Time in seconds allowed for direct indexation update on change. | 5                                                            |
| background_index_refresh_period_in_min   | integer | Period in minutes for background indexation.                 | 5                                                            |
| background_max_indexation_time_in_min    | integer | Execution time limit in minutes for background indexation.   | 5                                                            |
| background_index_full_rebuild_enabled    | boolean | Allow daily rebuild of the index.                            | true                                                         |
| background_index_full_rebuild_time       | hour    | Starting hour of the full rebuild of the index.              | '01:30'                                                      |

### Background behavior

*Searching for one word* When searching for a single word (example: *demo*) the following searches are done:

1. The word: *demo*
2. The words starting with the search: *demo**

*Searching for multiple words*

When searching for **multiple words**, (example: *user-level lock*) the following searches are done:

1. The exact sentence entered: *“user_level lock”*
2. All the words are present: *+user_level +lock*
3. At least one word is present: *user_level lock*

As `-` is a keyword to exclude a word, it is replaced by `_` which is another keyword to represent any single character.

*Computing weight*

Each search is bringing points calculated by MySQL fulltext search, which are then weighted with the configuration parameters set.

Raw weight is provided by MySQL. Parameters are just a multiplier factor of the MySQL weight. You cannot influence the raw weight within iTop.

### What values to set

To ensure that the search will be efficient within your iTop, there are additional actions for Administrator users:

- **Global search management** action which allow to rebuild the indexes after a change of configuration parameter: `object_weight_factor`.
- **Debug** action which display details on how the **result ordering** is generated, based on weight.

| [![img](https://www.itophub.io/wiki/media?media=extensions%3Aglobalsearchdebug.png)](https://www.itophub.io/wiki/media-detail?id=extensions%3Acombodo-fulltext-search&media=extensions%3Aglobalsearchdebug.png) | [![img](https://www.itophub.io/wiki/media?media=extensions%3Aglobalsearch-expend-search.png)](https://www.itophub.io/wiki/media-detail?id=extensions%3Acombodo-fulltext-search&media=extensions%3Aglobalsearch-expend-search.png) |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
|                                                              |                                                              |

- *user_level lock* has a MySQL provided weight
- *“user_level lock”* has the above weight * `sentence_weight_factor`
- *Total Score* is the sum of the various scores * `object_weight_factor`

Get from your users “sampling searches” on your real data, with the object expected to be in the top 5 results. Then change the various parameters, checking the result using the `Debug` action on those “sampling searches”.

## Usage

Just type the **words** in the global search field, then `enter` or click on the magnifier icon to get the result :

[![img](https://www.itophub.io/wiki/media?media=extensions%3Aglobalsearch-overviewuser.png)](https://www.itophub.io/wiki/media-detail?id=extensions%3Acombodo-fulltext-search&media=extensions%3Aglobalsearch-overviewuser.png)

### Tips to specify your search

Add `+` at the beginning of **required** word

```
UserRequest:+PHP error 
```

*will search for User Requests which contain mandatorily 'PHP' and maybe 'error'*

Add `-` at the beginning of **excluded** word

```
UserRequest:PHP -closed 
```

*will search for User Requests which contain 'PHP' but not 'closed' (this exclude all UserRequest with status=closed)*

Add `*` at the **end** of an **incomplete** word

```
Organization:Combo* Grenoble
```

*will search for Organization which contain a word starting with 'Combo' and the exact word 'Grenoble'. This is useless in single word search, as it does it automatically.*

### Restricting the search to a class

By default the search searchs on **all Classes** with *category* searchable, including abstract classes, such as Ticket, Contact or FunctionalCI.

| Restrict previous search to a single class                   | Expend back to all classes                                   |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [![img](https://www.itophub.io/wiki/media?media=extensions%3Aglobalsearch-restrictsearch.png)](https://www.itophub.io/wiki/media-detail?id=extensions%3Acombodo-fulltext-search&media=extensions%3Aglobalsearch-restrictsearch.png) | [![img](https://www.itophub.io/wiki/media?media=extensions%3Aglobalsearch-classsearch.png)](https://www.itophub.io/wiki/media-detail?id=extensions%3Acombodo-fulltext-search&media=extensions%3Aglobalsearch-classsearch.png) |
| [![img](https://www.itophub.io/wiki/media?media=extensions%3Aglobalsearch-expendsearch.png)](https://www.itophub.io/wiki/media-detail?id=extensions%3Acombodo-fulltext-search&media=extensions%3Aglobalsearch-expendsearch.png) |                                                              |

Add `<class-name>:` at the **beginning** of a search pattern to limit the search to objects of this classe or one of its descendants

```
FunctionalCI:combodo
```

*will search for any FunctionalCI which contains “combodo”, so the returned objects can be Server, PC, Enclosure,…*

The class name can be the internal name (like FunctionalCI) of the display name in the current language used (like CI fonctionnel).

### Displaying matching words

A menu allow to display some of the fields which have matched the requested pattern

[![img](https://www.itophub.io/wiki/media?w=600&tok=0fe437&media=extensions%3Aglobalsearch-matching-fields.png)](https://www.itophub.io/wiki/media-detail?id=extensions%3Acombodo-fulltext-search&media=extensions%3Aglobalsearch-matching-fields.png)

### Displaying related objects

On each returned object, you can request related objects: [![img](https://www.itophub.io/wiki/media?w=600&tok=24299c&media=extensions%3Aglobalsearch-relatedobject.png)](https://www.itophub.io/wiki/media-detail?id=extensions%3Acombodo-fulltext-search&media=extensions%3Aglobalsearch-relatedobject.png)