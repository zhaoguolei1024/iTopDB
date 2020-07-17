# Data Collector Base

- name:

  Data Collector Base

- description:

  Inventory Data Collector toolkit for creating your own data collectors for iTop

- version:

  1.1.4

- release:

  2020-07-07

- state:

  stable

- diffusion:

  Client Store, Combodo Site

This module provides the base for creating an industrial data collection and synchronization application for iTop. Developers can rely on this module to perform all the heavy lifting related to the iTop data import and synchronization process in order to focus on the data collection.

[Download 1.1.4](http://www.combodo.com/itop-extensions/itop-data-collector-base-1.1.4-592.zip)

## Features

- Simple API to make the creation of a new collector fast and easy.
- Automatic creation and update of Synchronization Data Sources in iTop, based on JSON definitions.
- Support small variations to the target Data Model via explicitely “Optional” attributes
- Basic validation of the CSV format compared to the expected fields in the synchro data source.
- Data upload and synchronization by chunks of `max_chunk_size` (configurable).
- Extensible mechanism for handling configuration parameters.
- Extensible list of placeholders in the JSON definition.
- Automatic management (via placeholders) of the contact to notify and the user to use for running the synchro.
- Validation of the minimum version of PHP and the needed extensions (as specified by the collector).
- Command line tool to produce the JSON definition from an existing Synchro Data Source in iTop.
- Capability to run independently: the configuration of the data sources, the data collection and the data synchronization.
- Configurable log level (for console output or syslog logging)
- Simple framework for quickly creating SQL based collectors

## Revision History

| Release Date | Version | Comments                                                     |
| ------------ | ------- | ------------------------------------------------------------ |
| 2020-06-24   | 1.1.4   | * The path to the configuration file can now be specified via the option `--config_file` on the command line. * The location where to store the collected data is now a parameter in the configuration file: `data_path`. * Better checking of Data Source definitions to catch missing reconciliation keys * Option on the Lookuptable class to treat lookup errors as normal |
| 2020-04-30   | 1.1.3   | * New CSV collector * Configurable timestamp added in the logs * New option for usage: –help |
| 2019-11-07   | 1.1.2   | Fix “undefined constant TABLENAME_PATTERN”                   |
| 2019-10-28   | 1.1.1   | Contains upgrades from both 1.0.13 and 1.1.0 * Reject invalid characters for database_table_name |
| 2019-10-28   | 1.1.0   | Based on 1.0.9 * Added the specific class MySQLCollector which forces the DB connection to use UTF-8 characters |
| 2019-10-28   | 1.0.13  | * LookupTables can now be non case sensitive (since MySQL is not) * Prevent a warning in SQLCollector for each “ignored” attribute * Improved support of iTop 2.4+ (obsolescence flag) |
| 2019-10-28   | 1.0.12  | * removed a warning in PHP 7.2                               |
| 2018-06-26   | 1.0.11  | Added a debug trace (visible if console_log_level=9) to show which mapping regular expression is applied (when one is applied). Bug fix: properly handle utf-8 characters in the mapping table's regular expressions (/u modifier) Make the cUrl/SSL options configurable to suit all possible combinations and security considerations. |
| 2015-06-30   | 1.0.10  | New class of collector: `MySQLCollector` which forces the retrieved data to be encoded in UTF-8. |
| 2015-06-09   | 1.0.9   | Performance enhancement: retrieve only the needed fields when building a lookup table. |
| 2015-06-02   | 1.0.8   | Better checking of files access rights for writing. SQL connection string (for SQL collectors) is now fully configurable. |
| 2015-05-20   | 1.0.7   | Bug fixes: Support of backslashes in file names. Removed a warning by marking Utils::Substitute() static. |
| 2015-05-13   | 1.0.6   | Added the support of “ignoring” some rows in the data while re-processing them. SQL collector can be configured to safely ignore some fields. |
| 2015-02-16   | 1.0.4   | Added the configuration parameter `stop_on_synchro_error`.   |
| 2015-01-06   | 1.0.3   | Handling of non UTF-8 data (via the overloading of GetCharset()), error checking for the data import phase, optimization for iTop 2.1.0: ignoring any change in the database_table_name field. |
| 2014-11-03   | 1.0.2   | Added the base class SQLCollector for easily creating SQL based collectors. |
| 2014-10-11   | 1.0.1   | Added the method `AttributeIsOptional` to handle variations in the target Data Model. |
| 2014-05-13   | 1.0.0   | First version                                                |

## Limitations

- Data upload to iTop is done only via the syncho_import web service (could use the command line version or direct SQLcommands. TBD later, maybe)
- Prior to the revision 3805 of iTop from SVN (from 2015-10-12!) the collector will **NOT** work properly if the account used to connect to iTop is not configured to use English as the language !!

## Requirements

- PHP Version 5.3.0 (support of namespaces may be required by some collectors)
- An access to the iTop web services (REST + synchro_import.php and synchro_exec.php)
- We recommand to install **php_curl** to use the collector base parameter `itop_synchro_timeout` otherwise the timeout is hardcoded to 200 secondes and can't be overwritten by the collector.

Under 1000 synchronized objects, it should work without `php_curl`, above it won't!

## Installation

- Expand the content of the zip archive on a folder on the machine were the collector will run.
- Edit the content of the file `conf/params.local.xml` to suit your installation.

## Configuration

`params.local.xml` is the only file to edit to configure a collector.

At minimum the following parameters must be set in this file:

```
  <itop_url>https://localhost/</itop_url>
  <itop_login>admin</itop_login>
  <itop_password>admin</itop_password>
```

| Parameter     | Meaning                                                      | Sample value           |
| ------------- | ------------------------------------------------------------ | ---------------------- |
| itop_login    | Login (user account) for connecting to iTop. Must have admin rights for executing the data synchro. | admin                  |
| itop_password | Password for the iTop account.                               |                        |
| itop_url      | URL to the iTop Application                                  | https://localhost/itop |

### Optional parameters

The following parameters can be redefined to alter the default behavior of the collector:

| Parameter              | Meaning                                                      | Default value    |
| ---------------------- | ------------------------------------------------------------ | ---------------- |
| max_chunk_size         | Maximum number of elements to process in one iteration (for upload and synchro in iTop). If there are more elements than this number, the process will automatically iterate. | 1000             |
| itop_synchro_timeout   | Timeout for waiting for the execution of one data synchro task (in seconds)- requires `php_curl` | 600              |
| stop_on_synchro_error  | Whether or not to stop when an error occurs during a synchronization (`yes` or `no`). | no               |
| console_log_level      | Level of ouput to the console. From -1 (none) to 9 (debug).  | 6 (info)         |
| console_log_dateformat | Logger timestamp format                                      | [Y-m-d H:i:s]    |
| curl_options           | When using cUrl to connect to the iTop Webservices the cUrl options can be specified in this section. The syntax is <CURLOPT_NAME_OF_THE_OPTION1>VALUE_1</CURLOPT_NAME_OF_THE_OPTION1> where VALUE_x are either: The numeric value of the option, or the string representation of the corresponding PHP “define” (case sensitive). It is possible to define several php_curl options like in the example below |                  |
| data_path              | **New in 1.1.4** The path where to store the temporary files generated by the collector. You can use the special placeholder `%APPROOT%` to specify a pth relative to the root folder of the collector. | `%APPROOT%/data` |

```
<curl_options>
    <CURLOPT_SSL_VERIFYHOST>0</CURLOPT_SSL_VERIFYHOST>
    <CURLOPT_SSL_VERIFYPEER>1</CURLOPT_SSL_VERIFYPEER>
  </curl_options>
```

The file `params.distrib.xml` contains the default values for the parameters. Both files (`params.distrib.xml` and `params.local.xml`) use exactly the same format. But `params.distrib.xml` is considered as the reference and should remain unmodified. Should you need to change the value of a parameter, copy and modify its definition in `params.local.xml`. The values in `params.local.xml` have precedence over the ones in `params.distrib.xml`

## Usage

To launch the data collection and synchronization with iTop, run the following command (from the root directory where the application is installed):

```
php exec.php
```

The following (optional) command line options are available:

| Option                      | Meaning                                                      | default value |
| --------------------------- | ------------------------------------------------------------ | ------------- |
| --config_file               | Specify the full path to the configuration file. The file `conf/params.local.xml` is used by default if this parameter is omitted. | empty         |
| --console_log_level=<level> | Level of ouput to the console. From -1 (none) to 9 (debug).  | 6 (info)      |
| --collect_only              | Run only the data collection, but do not synchronize the data with iTop | false         |
| --synchro_only              | Synchronizes the data previously collected (stored in the `data` directory) with iTop. Do not run the collection. | false         |
| --configure_only            | Check (and update if necessary) the synchronization data sources in iTop and exit. Do NOT run the collection or the synchronization |               |
| --max_chunk_size=<size>     | Maximum number of items to process in one pass, for preserving the memory of the system. If there are more items to process, the application will iterate. | 1000          |
| --help                      | Usage mode to display exec.php help.                         |               |

### Running several instances of the collector

In many circumstances it may be useful to run several times the collector with a different set of parameters. For example to collect persons information from several LDAP servers (iTop Data Collector for LDAP) or Virtual Machines information from several vSphere servers (iTop Data Collector for vSphere).

Prior to version 1.1.4 of the framework, you had to completely duplicate the collector application and adjust the file `conf/params.local.xml` on each copy.

Since version 1.1.4 you can have just one single copy the of the collector application and specify a different configuration file (with the command line option `--config_file`) for each collection to run (i.e. one configuration file per LDAP or vSphere server).

However, to avoid any troubles during the collection of the data and the synchronization with iTop, the following parameters must be properly configured inside the configuration file:

- Use a different `<prefix>` inside each different configuration file. This ensures that a specific set of Synchronization Data Sources will be created for each configuration file.
- Use a different `<data_path>` variable for each configuration file. This will cause the collector to store all its collected data (including some temporary files) in a dedicated directory. This prevents one instance of the collector to overwrite the data of another one. You can use the syntax `<data_path>%APPROOT%/data/collector1</data>` to have a subfolder `collector1` created inside the `data` folder.

------

# Creating a collector

The specifics about a collector resides inside the “collectors” folder. There must be at least one file `main.php` inside this folder. The purpose of `main.php` is to register all the `Collector` classes for your module and load the corresponding classes (either via `require_once(…)` or by registering an auto-loader).

A collector is a PHP class that provides the data for a given Synchronization Data Source. Collector classes are derived from the abstract `Collector` class. Each collector is associated with a Synchronization Data Source, defined in JSON format. The default implementation simply looks for a JSON file with the same name as the collector class and the extension “.json”, in the `collectors` folder.

### Specifying required extensions

If your collector needs a specific extension (or a minimum PHP version), you can indicate this dependency by calling the static method `Orchestrator::AddRequirement($sMinRequiredVersion, $sExtension = 'PHP')` in `main.php`:

For example:

```
Orchestrator::AddRequirement('5.4.0'); //This requires at least PHP 5.4
Orchestrator::AddRequirement('1.2.0', 'ldap'); //This requires at least the ldap extension version 1.2.0
```

### Creating the JSON definition file

The simpler way to create the JSON file for a Synchro Data Source, is to export the definition of an existing data source.

- Create the synchronisation data source in iTop, adjust its parameters (attributes, etc.) to suit your needs
- Use the command line tool `dump_tasks.php` (available in the `toolkit` folder to produce the JSON file:

```
php toolkit/dump_tasks.php --task_name="name of the task to export" > collectors/myCollector.json
```

Inside your data source definition you can use special placeholders to make the data source configurable by the user of the application, or to adjust its behavior via some special settings:

| Placeholder code      | Meaning                                                      | Sample value |
| --------------------- | ------------------------------------------------------------ | ------------ |
| `$version$`           | The version of the module. Useful for versioning your application, for example in the “description” of the synchro data source. | 1.0.0        |
| `$synchro_user$`      | The user to run the synchro, specified by its login in the configuration file. The identifier of the User object is available via this placeholder. | 12           |
| `$contact_to_notify$` | The contact to notify, specified by its email address in the configuration file. The identifer of the contact is supplied via this placeholder. | 48           |

On top of the 3 special configuration parameters listed above, all parameters defined in the section 'json_placeholders' of the configuration file are also available as placeholders inside the JSON file.

Sample configuration file:

- [params.local.xml](https://www.itophub.io/wiki/page?do=export_code&id=extensions%3Aitop-data-collector-base&codeblock=5)

  `<?xml version="1.0" encoding="UTF-8"?> <!--  Local values for parameters. --> <!--  The values defined in this file have precedence over the ones defined in params.distrib.xml --> <parameters>  <itop_url>https://localhost/trunk</itop_url>  <itop_login>admin</itop_login>  <itop_password>admin</itop_password>  <console_log_level>9</console_log_level>  <contact_to_notify>denis.flaven@combodo.com</contact_to_notify>  <synchro_user>admin</synchro_user>  <json_placeholders type="hash">    <test>Test 1</test>  </json_placeholders> </parameters>`

[Sample Synchro Data Source definition file](https://www.itophub.io/wiki/page?id=extensions%3Asample-collector-definition), notice the use of the `$version$`, `$synchro_user$`, `$contact_to_notify$` and `$test$` placeholders:

If you specify a non-empty value for `database_table_name`, this name **MUST BEGIN WITH** `<prefix>synchro_data`. Where `<prefix>` is the prefix used for all tables in iTop (configured using the `db_subname` parameter in the iTop configuration file).

If you modify the list of fields of a class already collected, you **must** update your JSON definition file, to specify what to do with the new fields. By default they are added to existing Data Synchro with `no update` and `no lock`.

## Implementing your collector

Your collector must be a class derived from `Collector`. It must implement (at least) the `Fetch()` method. Fetch must return either, for each object to load, an array using the format `attribute_code => value` or `false` when the end of the set of objects has been reached.

The array returned by `Fetch()` must contain:

- an entry `primary_key` that uniquely identifies the object being synchronized with iTop. The entry can contain whatever unique ID you can obtain from the inventory collection, or a unique identifier generated as a combination of the various fields of the object. It's up to the collector application to guarantee the unicity of this identifier (and its stability in time)
- an entry for each attribute of the object to be loaded in iTop.

The sample code below generates a set of 10 servers, named 'Server 1', 'Server 2' … 'Server 10', and initialized 3 fields of the servers: their name, their organization (always 'Demo') and their description.

- [main.php](https://www.itophub.io/wiki/page?do=export_code&id=extensions%3Aitop-data-collector-base&codeblock=6)

  `class MyCollector extends Collector {  protected $idx;   public function Prepare()  {        $bResult = parent::Prepare();        $this->idx = 0;        return $bResult;  }   public function Fetch()  {     if ($this->idx < 10)     {        $this->idx++;        return array(           'primary_key' => $this->idx,            'name' => 'Server '.$this->idx,            'org_id' => 'Demo',            'description' => 'Test Collector'        );     }     return false;  } }  // Register the collector, as the 1st to run Orchestrator::AddCollector(1, 'MyCollector');`

If the data returned by your collector are not encoded in the UTF-8 character set, overload the method `GetCharset()` of your collector to return the name of the character set (must return a value accepted by iconv on the iTop server)

### Registering your collector

To register your collector, call the static method `Orchestrator::AddCollector()`. The two parameters are:

- The order in which the collector should be run (when you need to run several collectors one after the other)
- The name of the class (derived from `Collector`) in which the collector is implemented.

### Default values for the parameters

A collector module can provide default values for its parameters by providing a file `params.distrib.xml` in the `collectors` folder. If such a file exists, its values are merged over the equivalent file in the `conf` directory.

## Existing Base Collectors

To create a new collector, you can base it on the standard or use one of those recently added Collectors which already does part of the job depending on your data source:

- CSV Collector
- SQL Collector
- *JSON Collector (to be released in 2021)*

### SQL Collectors

The 'core' folder provides an abstract class `SQLCollector` which can serve as the basis for quickly creating collectors that retrieve their data via a SQL query.

To create such a collector you need to:

1. Create a class derived from SQLCollector
2. Create the json definition file for the data synchro source
3. Add a configuration parameter (in `params.distrib.xml`) to define the SQL query to run
4. Register your collector in `collectors/main.php`

The configuration parameters for the SQL Collectors are:

| Parameter                            | Meaning                                                      | Default Value                |
| ------------------------------------ | ------------------------------------------------------------ | ---------------------------- |
| sql_engine                           | The [PDO driver/engine](http://php.net/manual/en/pdo.drivers.php) to use for the database connection. | mysql                        |
| sql_host                             | The name or IP address of the database server to connect to. | localhost                    |
| sql_database                         | The name of the database to connect to.                      | empty                        |
| sql_login                            | The login to use when connecting to the database             | root                         |
| sql_password                         | The password to use when connecting to the database          | n/a                          |
| sql_connection_string                | **New in 1.0.8** The format of the PDO connection string. 3 placeholders are available inside the format string: `%1$s` = *sql_engine*, `%2$s`= *sql_database* and `%3$s` = *sql_host* | `%1$s:dbname=%2$s;host=%3$s` |
| *collector_class*_query              | The query to run for the collector which PHP class is *collector_class* |                              |
| *collector_class*_ignored_attributes | **New in 1.0.6** To take into account the possible variations of the data model, without re-writing a collector each time, it is possible to mark some of the collected attributes as “optional” so that the collector can run even if the corresponding attribute does not exist in the data model. Supply an array of attribute codes to ignore, here. |                              |

To specify a port number (or any other driver specific options), change the format of the `sql_connection_string`. For example: `%1$s:dbname=%2$s;host=%3$s;port=3307`

For versions prior to 1.0.8, to specify a port number (other than the default port), use the syntax `host;port=xxxx` for the `sql_host` parameter. Example: `localhost;port=3307`

Starting with version 1.0.10, the framework provides a new class of collector: `MySQLCollector`. This class is identical to `SQLCollector` except that it forces the retrieved data to be encoded in UTF-8 by issuing the SQL command `SET NAMES 'utf8`' at the beginning of the each connection to the database. To avoid any problem with the character set of the data, it is recommended to use this new class for all connections to a MySQL/MariaDB database.

#### Example of a simple SQL Collector

Let's create a very simple SQL collector which copies the “Notes” documents (class DocumentNote) from one iTop instance to another. Since the collector inherits all its behavior from the base class, the PHP code for the collector is simply:

- [DocumentNotesCollector.class.inc.php](https://www.itophub.io/wiki/page?do=export_code&id=extensions%3Aitop-data-collector-base&codeblock=7)

  `<?php class DocumentNoteCollector extends SQLCollector { }`

Find here a sample of an [SQL collector definition](https://www.itophub.io/wiki/page?id=extensions%3Asample-collector-sql) file.

Then in `params.distrib.xml`, add the following entries:

```
  <sql_database>test</sql_database>
  <sql_login>root</sql_login>
  <sql_password>s3cret</sql_password>
  <documentnotecollector_query>SELECT id as primary_key, name, text, description, status, '2.0' as version, documenttype_id, 1 as org_id FROM view_DocumentNote</documentnotecollector_query>
  <documentnotecollector_ignored_attributes type="array">
    <attribute>location_id</attribute>
    <attribute>version_id</attribute>
  </documentnotecollector_ignored_attributes>
```

Finally, in `collectors/main.php` add the following lines:

- [main.php](https://www.itophub.io/wiki/page?do=export_code&id=extensions%3Aitop-data-collector-base&codeblock=9)

  `<?php require_once(APPROOT.'collectors/DocumentNoteCollector.class.inc.php'); Orchestrator::AddCollector(1 /* $iRank */, 'DocumentNoteCollector');`

### CSV Collector

The 'core' folder provides an abstract class `CSVCollector` which can serve as the basis for quickly creating collectors that retrieve their data from CSV files.

To create such a collector you need to:

1. Create a class derived from CSVCollector
2. Create the json definition file for the data synchro source
3. Add a configuration parameter (in `params.distrib.xml`) to define the CSV file to parse
4. Register your collector in `collectors/main.php`

The configuration parameters for the CSV Collectors are:

| Parameter                   | Meaning                                                      | Default Value |
| --------------------------- | ------------------------------------------------------------ | ------------- |
| *collector_class*_csv       | The csv file to parse for the collector which PHP class is. You can specify the full path of this file (/tmp/myfile.csv) or a relative path to the collector *collector_class*. This parameter is mandatory |               |
| *collector_class*_command   | The CLI command to execute BEFORE parsing csv file for the collector which PHP class is *collector_class*. This parameter is optional |               |
| *collector_class*_encoding  | The csv file encoding for the collector which PHP class is *collector_class*. This parameter is optional | UTF-8         |
| *collector_class*_separator | The separator to use for the csv file to parse. This parameter is optional | ;             |

#### Example of a simple CSV Collector

Let's create a very simple CSV collector which copies the “Person” objects (class Person)

Since the collector inherits all its behavior from the base class, the PHP code for the collector is simply:

- [iTopPersonCsvCollector.class.inc.php](https://www.itophub.io/wiki/page?do=export_code&id=extensions%3Aitop-data-collector-base&codeblock=10)

  `<?php class iTopPersonCsvCollector extends CSVCollector { }`

Find here a [sample of Collector definition for CSV](https://www.itophub.io/wiki/page?id=extensions%3Asample-collector-csv)

Then in `params.distrib.xml`, add the following entries:

```
<?xml version="1.0" encoding="UTF-8"?>
<parameters>
  <iTopPersonCsvCollector_csv>collectors/iTopPersonCsvCollector.csv</iTopPersonCsvCollector_csv>
  <iTopPersonCsvCollector_command>sed -i -e 's|isaac|ISAAC|g' collectors/iTopPersonCsvCollector.csv</iTopPersonCsvCollector_command>
  <iTopPersonCsvCollector_encoding>UTF-8</iTopPersonCsvCollector_encoding>
</parameters>
```

Finally, in `collectors/main.php` add the following lines:

- [main.php](https://www.itophub.io/wiki/page?do=export_code&id=extensions%3Aitop-data-collector-base&codeblock=12)

  `<?php require_once(APPROOT.'collectors/iTopPersonCsvCollector.class.inc.php'); Orchestrator::AddCollector($index++, 'iTopPersonCsvCollector');`

### JSON Collector

The 'core' folder provides an abstract class `JSONCollector` which can serve as the basis for quickly creating collectors that retrieve their data from JSON files.

To create such a collector you need to:

1. Create a class derived from JSONCollector
2. Create the json definition file for the data synchro source
3. Add a configuration parameter (in `params.distrib.xml`) to define the JSON file to parse
4. Register your collector in `collectors/main.php`

The configuration parameters for the JSON Collectors are:

| Parameter                  | Meaning                                                      |
| -------------------------- | ------------------------------------------------------------ |
| *collector_class*_jsonfile | Define relative or absolute path to the json file to parse for the collector which PHP class is collector *collector_class*. This parameter or *collector_class*_jsonurl is mandatory |
| *collector_class*_jsonurl  | The URL of json file to parse for the collector which PHP class is. This parameter or *collector_class*_jsonpath is mandatory |
| *collector_class*_jsonpost | Xml of params to post with the url in order to get Json file *<name_of_param>value</name_of_param>* |
| *collector_class*_command  | The CLI command to execute BEFORE parsing json file for the collector which PHP class is *collector_class*. This parameter is optional |
| *collector_class*_way      | way in order to find data to synchronize in json separator is / and * replace any word *by example aa/bb for {“aa”:{“bb”:{mydata},“cc”:“xxx”} and aa/ \* /bb for {“aa”:{cc“:{“bb”:{mydata1}},”dd“:{“bb”:{mydata2}}}* |
| *collector_class*_fields   | xml witch describe connection between name in json and name in itop *<name_in_json>name_in_itop</name_in_json>* |

#### Example of a simple JSON Collector

Let's create a very simple JSON collector which copies the “Person” objects (class Person) from one iTop to another

Since the collector inherits all its behavior from the base class, the PHP code for the collector is simply:

- [ITopPersonJsonCollector.class.inc.php](https://www.itophub.io/wiki/page?do=export_code&id=extensions%3Aitop-data-collector-base&codeblock=13)

  `<?php class ITopPersonJsonCollector extends JsonCollector { }`

Find here a sample for [Collector definition file](https://www.itophub.io/wiki/page?id=extensions%3Asample-collector-json) for JSON

Then in `params.distrib.xml`, add the following entries:

```
<?xml version="1.0" encoding="UTF-8"?>
<parameters>
        <itoppersonjsoncollector_jsonurl>http://localhost/iTop/webservices/rest.php</itoppersonjsoncollector_jsonurl>
        <itoppersonjsoncollector_jsonpost>
                <auth_user>restuser</auth_user>
                <auth_pwd>restuserpassword</auth_pwd>
                <json_data>{"operation": "core/get", "class": "Person", "key": "SELECT Person WHERE email LIKE '%.com'", "output_fields": "friendlyname, email, first_name, function, name, id, org_id,phone"}</json_data>
                <version>1.3</version>
        </itoppersonjsoncollector_jsonpost>
        <itoppersonjsoncollector_way>objects/*/fields</itoppersonjsoncollector_way>
        <itoppersonjsoncollector_fields>
                <primary_key>id</primary_key>
                <name>name</name>
                <status>status</status>
                <first_name>first_name</first_name>
                <email>email</email>
                <phone>phone</phone>
                <mobile_phone>mobile</mobile_phone>
                <function>function</function>
                <employee_number>employee_number</employee_number>
                <org_id>org_id</org_id>
        </itoppersonjsoncollector_fields>
        <itoppersonjsoncollector_defaults>
                <org_id>Demo</org_id>
                <status>active</status>
        </itoppersonjsoncollector_defaults>
        <json_placeholders>
                <!-- For compatibility with the version 1.1.x of the collector, define the data table names as following:
             <prefix></prefix>
             <persons_data_table>synchro_data_PersonAD</persons_data_table>
             <users_data_table></users_data_table>
              -->
                <prefix>$prefix$</prefix>
                <persons_data_table>synchro_data_person</persons_data_table>
        </json_placeholders>
</parameters>
```

Finally, in `collectors/main.php` add the following lines:

- [main.php](https://www.itophub.io/wiki/page?do=export_code&id=extensions%3Aitop-data-collector-base&codeblock=15)

  `<?php require_once(APPROOT.'collectors/ITopPersonJsonCollector.class.inc.php'); Orchestrator::AddCollector($index++, 'ITopPersonJsonCollector');`

## Advanced collectors

The collector framework provides means to perform some advanced processing for real-life collectors:

- DataMapping for configurable data normalizations
- LookupTable for advanced reconciliations based on multiple fields

### Data Mapping

Raw data collected by inventory scripts sometimes require a normalization before being imported into iTop, in order to obtain homogenous data. The framework provides the helper class `MappingTable` for performing simple normalizations tasks.

A mapping table is configured (in the `params.xxx.xml` configuration file) as an ordered list of patterns, with a value associated to each pattern. The “clean” value returned by the mapping table is the value associated with the first pattern that matches the input value. Patterns are expressed as regular expressions. Values can use the placeholders to refer to some part of the matched pattern (`%1$s` is the whole pattern, `%2$s` the first group inside the regular expression, etc.).

Example of configuration (Brand normalization):

```
  <brand_mapping type="array">
    <!-- Syntax /pattern/replacement where:
      any delimiter can be used (not only /) 
      but the delimiter cannot be present in the "replacement" string
      pattern is a RegExpr pattern
      replacement is a sprintf string in which:
          %1$s will be replaced by the whole matched text,
          %2$s will be replaced by the first matched group, if any group is defined in the RegExpr
          %3$s will be replaced by the second matched group, etc...
    -->
    <pattern>/IBM/IBM</pattern>
    <pattern>/Hewlett.Packard/Hewlett-Packard</pattern>
    <pattern>/Dell/Dell</pattern>
    <pattern>/.*/%1$s</pattern>
  </brand_mapping>
```

This example file performs the following normalization:

1. Every string containing “IBM” is transformed into “IBM”,
2. Every string containing “Hewlett”, followed by any character, followed by “Packard” is transformed into “Hewlett-Packard”,
3. Every string containing “Dell” is transformed into “Dell”,
4. All other strings are kept as is.

#### Using a mapping table in your code

1. Create an instance of the `MappingTable` class, passing it the name of the XML tag in which to look for its configuration (inside the XML param file)
2. Use the `MapValue` method to process each value as needed (the second parameter is the default value, when no match is found in the mapping table).

Usage example:

```
// Turns the raw brand string ('brand_id') into a normalized brand
// Use 'Other' for brands not found in the normalization table
 
class TestCollector extends SQLCollector
{
    protected $oBrandMapping;
 
    public function Prepare()
    {
        $bRet = parent::Prepare();
        // Create the MappingTable once at the initialization of your collector
        $this->oBrandMapping = new MappingTable('brand_mapping');
        return $bRet;
    }
 
    public function Fetch()
    {
        $aData = parent::Fetch();
        if ($aData !== false)
        {
            // Then process each collected brand
            $aData['brand_id'] = $this->oBrandMapping->MapValue($aData['brand_id'], 'Other');
        }
        return $aData;
    }
}
```

### Advanced Lookups

The data synchronization mechanism embedded in iTop is not capable of performing reconciliations based on multiple fields (like searching for a Model based on both the Brand name and the Model name). The `LookupTable` class provides this reconciliation capability for any number of fields.

The class `LookupTable` builds a lookup table by retrieving the specified fields of a set of iTop objects, and storing the resulting identifier of the objects in iTop.

An instance of `LookupTable` is created by specifying an OQL query (the set of iTop objects to retrieve) and the fields of the objects that will be used for the mapping.

The list (and the order) of the fields specified during the creation of the `LookupTable` instance is the list of fields to be passed later on when performing a `Lookup(…)`

Once the `LookupTable` has been initialized, a call to the `Lookup($aData, array(Field1, Field2, …), destField)` method will replace in `$aData` the value of the column `destField` by identifier of the iTop object whose specified fields match the values passed in `$aData` as the columns `Field1, Field2…`.

**Since version 1.0.6**, the `Lookup` method returns false if not corresponding lookup was found. In such a case the code can either supply a default value, of throw an exception `IgnoredRowException` to tell the collector to reject the whole line of collected data.

**Since version 1.1.4**, the constructor of `LookupTable` accepts one extra (optional) parameter: `$bIgnoreMappingErrors` (default to `false`). If this parameter is set to `true`, the `LookupTable` will consider that lookup errors are *normal* and will not report them as warnings (but still list them in debug mode). This can be useful when the Lookuptable is used for filtering the collected data against a catalog defined in iTop. In such a case, lookup errors are the expected behavior.

#### Example

In iTop, the operating system version is represented as a `version` depending on an `OS family` object. We can have the following objects in iTop:

- Windows, versions 7.0 and 8.1,
- Debian version 12.0.0.

This will be stored in iTop as shown below:

| Object class | id   | name         |
| ------------ | ---- | ------------ |
| OSFamily     | 1    | Windows      |
| OSFamily     | 2    | Linux Debian |

| Object class | id   | osfamily_id | name   |
| ------------ | ---- | ----------- | ------ |
| OSVersion    | 1    | 1           | 7.0.0  |
| OSVersion    | 2    | 1           | 8.1.0  |
| OSVersion    | 3    | 2           | 12.0.0 |

Now let's imagine that our collector script gives us the two informations: 'Windows' and '8.1.0'. We can store the 'Windows' text string in the 'osfamily_id' field of the data synchro table and configure the synchro data source to perform the reconciliation based on the 'name' (this will properly replace 'Windows' by 1).

But to retrieve the identifier of the version 8.1.0 of Windows (which is 2 in our example) we need *both* the OS Family ('Windows') and the version number ('8.1.0'). The Synchronization Data Source is not capable of doing this *composite* lookup, this where the `LookupTable` comes into play.

```
$oOSVersionLookup = new LookupTable('SELECT OSVersion', array('osfamily_id_friendlyname', 'name'));
```

This will build - in memory - the following table:

| lookup_key    | id   |
| ------------- | ---- |
| Windows_7.0.0 | 1    |
| Windows_8.1.0 | 2    |
| Debian_12.0.0 | 3    |

So if we have in `$aData` the following values:

| osfamily_id | osversion_id |
| ----------- | ------------ |
| Windows     | 8.1.0        |

Calling:

```
$oOSVersionLookup->Lookup($aData, array('osfamily_id', 'osversion_id'), 'osversion_id', 0);
```

Will place in the column 'osversion_id' the result of the lookup for the values `$aData['osfamily_id']` and `$aData['osversion_id']`.

`$aData` will then contain the following values:

| osfamily_id | osversion_id |
| ----------- | ------------ |
| Windows     | 2            |

We then have to configure the Synchro Data Source so that it accepts the `oversion_id` as-is without performing any reconciliation on it.

The last parameter of `Lookup(…)` must contain the line number inside the CSV file being processed. This is used internally to perform some initializations only once when processing the first line of the file.

The advanced reconciliation works by retrieving (via the REST/JSON API), the objects to be matched against the composite key, *after* the data collection but *before* pushing the data to iTop. Therefore, in order to use this advanced lookup mechanism, you *must* tell the framework that the collector has to reprocess the collected data before the actual synchro. This is achieved by overloading the method `MustProcessBeforeSynchro` of the collector; and returning `true`.

The collector framework provides two additional methods which can be overloaded:

1. `InitProcessBeforeSynchro` is called *after* the data collection, but before starting to reprocess each line of the collected data. This is the plece where to create the `LookupTable` instance
2. `ProcessLineBeforeSynchro` is called for each line of the collected data (including the header line of the CSV file, which index is zero)

#### Usage Example

The following code fragment shows to use cases of lookup tables altogether: one for brand + model and one for OS family + OS version.

```
protected function MustProcessBeforeSynchro()
{
        // We must reprocess the CSV data obtained from the inventory script
        // to lookup the Brand/Model and OSFamily/OSVersion in iTop
        return true;
}
 
protected function InitProcessBeforeSynchro()
{
        // Retrieve the identifiers of the OSVersion since we must do a lookup based on two fields: Family + Version
        // which is not supported by the iTop Data Synchro... so let's do the job of an ETL
        $this->oOSVersionLookup = new LookupTable('SELECT OSVersion', array('osfamily_id_friendlyname', 'name'));          
 
        // Retrieve the identifiers of the Model since we must do a lookup based on two fields: Brand + Model
        // which is not supported by the iTop Data Synchro... so let's do the job of an ETL
        $this->oModelLookup = new LookupTable('SELECT Model', array('brand_id_friendlyname', 'name'));             
}
 
protected function ProcessLineBeforeSynchro(&$aLineData, $iLineIndex)
{
        // Process each line of the CSV
        if (!$this->oOSVersionLookup->Lookup($aLineData, array('osfamily_id', 'osversion_id'), 'osversion_id', $iLineIndex))
        {
            throw New IgnoredRowException('Unknown OS Version');
        }
        if (!$this->oModelLookup->Lookup($aLineData, array('brand_id', 'model_id'), 'model_id', $iLineIndex))
        {
            throw New IgnoredRowException('Unknown Model');
        }
}
```

#### Data Model Variants

It may happen that the target Data Model has some variants (depending on the set of modules chosen during the installation). If a given attribute can be missing in some configurations, you can tell your collector to accept this variation, by overloading the method `AttributeIsOptional`. (This is simpler than writing a specific collector for each combination).

If an attribute specified in the JSON definition of the Synchro Data Source is missing, the processing will stop with an error, unless this attribute is declared as optional. In the later case, the name of the skipped attribute is recorded in the protected member variable `$this->aSkippedAttributes` and the processing continues. The code of the collector can later check the content of the array `$this->aSkippedAttributes` to determine which fields have to be collected or not.

Example of implementation of `AttributeIsOptional` as a method of the `VirtualMachineCollector` class:

```
public function AttributeIsOptional($sAttCode)
{
        // If the module Service Management for Service Providers is selected during the setup
        // there is no "services_list" attribute on VirtualMachines. Let's safely ignore it.
        if ($sAttCode == 'services_list') return true;
 
        return parent::AttributeIsOptional($sAttCode);
}
```

#### Troubleshooting

When troubleshooting the reconciliation mechanism it is useful to compare the original (raw) values as reported by the inventory script with the result of the reconciliation process. Whenever the method `MustProcessBeforeSynchro` of a collector returns `true`, the framework generates two files inthe `data` subdirectory. You can easily compare the values before/after the lookup by comparing the two CSV files:

1. `<collector_name>.raw-<index>.csv`: the original data, as produced by the inventory script,
2. `<collector_name>-<index>.csv`: the reprocessed data, to be uploaded to iTop.