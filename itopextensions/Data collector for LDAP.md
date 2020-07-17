# Data collector for LDAP

- name:

  Data collector for LDAP

- description:

  Inventory Data Collector for LDAP

- version:

  1.2.2

- release:

  2020-07-07

- diffusion:

  iTop Hub, Combodo site

- code:

  ldap-data-collector

- standalone:

  yes

This stand-alone application collects information from a **single** LDAP Directory in order to automatically synchronize the persons and the users in iTop.

![Data collector for LDAP](https://www.itophub.io/wiki/media?media=extensions%3Aldap_collector.png)

## Features

Main functions:

- Automatic creation and update of Persons and Users in iTop based on LDAP data.
- Automatic assignment of Profiles to Users based on LDAP groups (this is optional).
- 

Technical aspects:

- The collector can reside on any system with web access to iTop and LDAP access to the LDAP Directory
- The collector is compatible with Windows Active Directory
- The definition of the mapping between LDAP fields and iTop fields is fully configurable.
- The creation of the Synchronization Data Sources in iTop is fully automated.

This collector makes use of iTop's built-in Data Synchronization mechanism. For more information about how the data synchronization works, refer to [Data Synchronization Overview](https://www.itophub.io/wiki/page?id=latest%3Aadvancedtopics%3Adata_synchro_overview) and relies on [Data collector Base](https://www.itophub.io/wiki/page?id=extensions%3Aitop-data-collector-base) mechanism

## Revision History

| Version    | Release Date | Comments                                                     |
| ---------- | ------------ | ------------------------------------------------------------ |
| 2020-07-07 | 1.2.2        | Support of LDAP URI scheme for the connection, Better debug information via ldap-test.php, Configurable target class to create either users of type UserLDAP or UserExternal for example. Request only the needed attributes (and explicitely request memberof) Additional command line parameters for `ldap_test.php` Multi configuration file New CSV collector Configurable timestamp added in the logs New option for usage: –help |
| 2020-02-17 | 1.2.1        | Never publicly released, only updates to data collector base. Fix “undefined constant TABLENAME_PATTERN” Reject invalid characters for database_table_name Performance enhancement: retrieve only the needed fields when performing a lookup Added the specific class MySQLCollector which forces the DB connection to use UTF-8 characters |
| 2018-08-28 | 1.2.0        | First public release on iTopHub, refactoring of the code and configuration parameters. |
| 2017-06-22 | 1.1.1        | Version to use latest version of collector-base              |
| 2015-05-29 | 1.1.0        | Version to fix UTF8 encoding issue                           |
| 2015-05-07 | 1.0.0        | Initial version                                              |

## Limitations

- The current version is synchronizing neither the Organizations nor the Locations.
- The location of person and the manager of a person are not synchronized.
- One collector is collecting data from one single LDAP directory instance only.

## Requirements

- PHP (command line interface), version 5.3.0 up to 7.2 with the `php-ldap`, `php-dom` and `php-simplexml` extensions installed.
- An LDAP access to the Enterprise directory and a read user to access the data.
- An HTTP/HTTPS access to the iTop web services (REST + synchro_import.php and synchro_exec.php)
- \+ [Data collector Base](https://www.itophub.io/wiki/page?id=extensions%3Aitop-data-collector-base#requirements) requirements.

## Installation

- Expand the content of the zip archive “ldap-data-collector” in a folder on the machine that will run the collector application. This machine *must* have an LDAP access to the Enterprise directory and a web access to the iTop server.
- create the file `conf/params.local.xml` to suit your installation, supplying the appropriate credentials to connect to LDAP server and iTop.

By default this file should contains the values used to connect to the LDAP server and to the iTop server:

- [params.local.xml](https://www.itophub.io/wiki/page?do=export_code&id=extensions%3Aldap-data-collector&codeblock=0)

  `<?xml version="1.0" encoding="UTF-8"?> <!-- conf/params.local.xml - your specific configuration parameters --> <parameters>  <itop_url>http://localhost/</itop_url>  <itop_login>admin</itop_login>  <itop_password>admin</itop_password>  <contact_to_notify>john.doe@demo.com</contact_to_notify>  <synchro_user>admin</synchro_user>  <ldapuri>ldap://localhost:389</ldaphost>  <ldapdn>DC=company,DC=com</ldapdn>  <ldaplogin>CN=ITOP-LDAP,DC=company,DC=com</ldaplogin>  <ldappassword>password</ldappassword>  <!--    Set a non empty (and unique) prefix if you run several instances of the collector against the same iTop Server    This is the recommended method to collect data from several LDAP servers. (assign a unique prefix to each "source" LDAP server)    Note: this prefix can be set but do not touch the one inside json_placeholders    -->  <prefix></prefix>  <json_placeholders>    <full_load_interval>604800</full_load_interval><!-- 7 days (in seconds): 7*24*60*60 -->    <users_target_class>UserLDAP</users_target_class>    <synchro_status>production</synchro_status>  </json_placeholders> </parameters>`

| Parameter          | Meaning                                                      | Sample value                   |
| ------------------ | ------------------------------------------------------------ | ------------------------------ |
| itop_url           | URL to the iTop Application                                  | https://localhost/             |
| itop_login         | Login (user account) for connecting to iTop. Must have rights for executing the data synchro, to create Persons and Users (and connect to REST services on iTop above 2.5.0) | admin                          |
| itop_password      | Password for the iTop account.                               |                                |
| contact_to_notify  | The email address of an existing contact in iTop, to be notified in case of error during the synchronization | john.doe@demo.com              |
| synchro_user       | iTop user set as allowed to run synchronization. It is highly recommended to use the same as itop_login | admin                          |
| ldaphost           | **obsolete**, Use `ldapuri` instead.                         | localhost                      |
| ldapport           | **obsoelete**, use `ldapuri` instead.                        | 389                            |
| ldapdn             | Company DN for LDAP                                          | DC=company,DC=com              |
| ldaplogin          | Login to connect to LDAP server                              | CN=ITOP-LDAP,DC=company,DC=com |
| ldappassword       | Password to connect to LDAP server                           |                                |
| ldapuri            | The URI to connect to the LDAP server, either ldap://<host>:<port> or ldaps://<host>:<port> |                                |
| prefix             | A unique string for each LDAP server. MUST be non-empty if you run several instances of the collector against the same iTop instance. Can contain only [a-z0-9_] characters. |                                |
| full_load_interval | Duration (in seconds) for which to retain records not found in LDAP. |                                |
| synchro_status     | For information: the status of the Synchronization Data Sources (production, implementation or obsolete) | production                     |
| users_target_class | The class of User objects to create in iTop when synchronizing users. Either UserLDAP or UserExternal | UserLDAP                       |

Starting with iTop version 2.5.0, the account used to connect to iTop **must have** the profile `REST Services user` in order to be allowed to use the web services.

Before iTop version 2.5.0, only `Administrators` users can create Users

## Configuration

The default values for the configuration of the data collection is defined in the file collectors/params.distrib.xml. This configuration defines which LDAP queries are executed on the LDAP server to retrieve the data, how to map the LDAP fields with the iTop fields and some default values for the iTop fields.

The file `params.distrib.xml` contains the default values for the parameters, it's the reference and should remain unmodified.
The file `params.local.xml` contains the values **you have defined**. They have precedence over the default values defined in `params.distrib.xml`
Both files use exactly the same format.

The configuration looks as follows:

```
<parameters>
        <!-- Parameters for Person synchronization -->
        <ldappersonfilter>(objectClass=person)</ldappersonfilter>
        <person_fields>
                <!--  Mapping between LDAP fields and iTop Person's object fields -->
                <primary_key>samaccountname</primary_key>
                <name>sn</name>
                <first_name>givenname</first_name>
                <email>mail</email>
                <phone>telephonenumber</phone>
                <mobile_phone>mobile</mobile_phone>
                <function>title</function>
                <employee_number>employeenumber</employee_number>
        </person_fields>
        <person_defaults>
                <!--  Default values for iTop Person's object fields -->
                <org_id>Demo</org_id>
                <status>active</status>
        </person_defaults>
        <!-- Parameters for User synchronization -->
        <collect_person_only>no</collect_person_only>
        <ldapuserfilter>(&amp;(objectClass=person)(mail=*))</ldapuserfilter>
        <synchronize_profiles>no</synchronize_profiles>
        <itop_group_pattern>/^CN=itop-(.*),OU=.*/</itop_group_pattern>
        <user_fields>
                <!--  Mapping between LDAP fields and iTop UserLDAP's object fields -->
                <primary_key>samaccountname</primary_key>
                <login>samaccountname</login>
                <contactid>mail</contactid>
        </user_fields>
        <user_defaults>
                <!--  Default values for iTop UserLDAP's object fields -->
                <profile>Portal user</profile>
                <language>EN US</language>
        </user_defaults>
</parameters>
```

| Parameter            | Meaning                                                      | Default value                                                |
| -------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| ldappersonfilter     | The LDAP query used to retrieve the persons in LDAP/AD       | (objectClass=person)                                         |
| person_fields        | The list of iTop fields of the Person object to populate from the LDAP data, and for each iTop field its mapping to the corresponding LDAP field | `<person_fields>  <primary_key>samaccountname</primary_key>  <name>sn</name>  <first_name>givenname</first_name>  <email>mail</email>  <phone>telephonenumber</phone>  <mobile_phone>mobile</mobile_phone>  <function>title</function>  <employee_number>employeenumber</employee_number> </person_fields>` |
| person_defaults      | The default values for some iTop fields for a Person. Used either when the LDAP query returns an empty value or if no mapping is defined for the field | `<person_defaults>  <org_id>Demo</org_id>  <status>active</status> </person_defaults>` |
| collect_person_only  | Whether or not to synchronize users from LDAP (yes/no)       | no                                                           |
| ldapuserfilter       | The LDAP query to use to retrive user information in LDAP. *Note: the ampersand character `&` is a special character in XML and must be written as `&`* | (&amp;(objectClass=person)(mail=*))                          |
| synchronize_profiles | Flag to activate or not synchronization of the user profiles based on defined LDAP groups. If set to yes, the synchronization of the profiles is using the itop_group_pattern to identify corresponding group. If set to no make sure that you specify a default profile, since users cannot be created without at least one profile. | no                                                           |
| itop_group_pattern   | Regular expression pattern to retrieve list of LDAP group to map with iTop profils. The first capturing group (i.e. parentheses) must return the name of an existing iTop profile. The default regular expression looks for groups named `itop-<iTop Profile Name>` | `/^CN=itop-(.*),OU=.*/`                                      |
| user_fields          | The list of iTop fields for the LDAPUser object, to populate from the LDAP data, and for each iTop field its mapping to the corresponding LDAP field | `<user_fields>  <primary_key>samaccountname</primary_key>  <login>samaccountname</login>  <contactid>mail</contactid> </user_fields>` |
| user_defaults        | The default values for some iTop fields for a UserLDAP. Used either when the LDAP query returns an empty value or if no mapping is defined for the field. | `<user_defaults>  <profile>Portal user</profile>  <language>EN US</language> </user_defaults>` |

Those parameters can be redefined in the file `conf/params.local.xml` in order to take into account your specific needs. (For instance the mapping between iTop and LDAP attributes)

The expected value for `person_defaults/org_id` is an organization name, not an id

The expected value for `user_fields/login` can be UID, samaccountname, mail,… but the field must contain unique values

The expected value for `user_fields/contactid` is a field containing an **email address**

`user_defaults/profile` is a shortcut to fill the LDAP User field named `profile_list` with one unique profile.
If you want to assign several profiles to the LDAP Users, use the tag `profile_list` with this format:

```
<user_defaults>
  <profile_list>profileid->name:name_of_profile1|profileid->name:name_of_profile2</profile_list>
  ...
```

## Troubleshooting

### Connection problems

To test and troubleshoot connection problems, use the script `ldap-test.php` located in the `collector/bin` folder. The script uses the same parameters as the normal collector, but produces more debug output.

So edit the configuration in the file `conf/params.local.xml` then launch the test script by typing the following command from the command prompt.

```
php collectors/bin/ldap-test.php
```

If you see a message like:

```
Error - ldap_bind('cn=admin,dc=combodo,dc=com', '*******') FAILED (Can't contact LDAP server).
```

then something is wrong with the connection to the LDAP server.

1. Check that parameter `<ldapuri>` is correct. (protocol, host and port)
2. Check that the connection to the server is not blocked by a firewall (You can use the command `telnet <host> <port>` and see if the connection is established).
3. Check for TSL/SSL problems. If you see the following text in the output of the `ldap-test.php` script, then the problem is likely related to a TLS certificate:

```
attempting to connect: 
connect success
TLS: peer cert untrusted or revoked (0x402)
TLS: can't connect: (unknown error code).
```

The solution is to instruct LDAP to ignore this faulty certificate, by adding the following lines to the *LDAP configuration file* (see the note below).

```
# Ignore the server's certificate
TLS_REQCERT never
```

On Linux systems; the OpenLDAP library used by PHP tries to load successively the following configuration files:

1. /etc/ldap/ldap.conf
2. /home/<current_user>/ldaprc
3. /home/<current_user>/.ldaprc
4. <current_folder>/ldaprc

You can put the above mentioned parameter in any of the files, but be aware that the first file (/etc/ldap/ldap.conf) affects the whole system, whereas the other configuration files affect scripts running under the current user, or only scripts ran from the current directory.

The syntax for all thoses files is the same. For more information, refer to: [ldap.conf man page](https://www.openldap.org/software/man.cgi?query=ldap.conf)

### Data collection problems

If the output of the `ldap-test.php` script contains:

```
Error - ldap_search('dc=combodo,dc=net', '(objectClass=inetOrgPerson)') FAILED (No such object).
```

Then check the LDAP query used for retrieving the “contacts”. This query is defined by the two parameters:

```
    <ldapdn>DC=company,DC=com</ldapdn>
 
    <!-- Parameters for Person synchronization -->
    <ldappersonfilter>(objectClass=person)</ldappersonfilter>
```

If the LDAP query is correct, you should see an output similar to:

```
List of the attributes to retrieve (taken from the mapping):
uid,sn,givenname,mail,telephonenumber,mobile,title,employeenumber,memberof
Use --attributes=x,y,z to retrieve x, y and z instead. Use --attributes=* to retrieve all fields.
Debug - ldap_connect('ldaps://customers.combodo.com')...
Debug - ldap_bind('cn=admin,dc=combodo,dc=com', 'c8mb0do')...
Debug - ldap_bind() Ok.
Debug - ldap_search('dc=combodo,dc=com', '(objectClass=inetOrgPerson)', ['uid', 'sn', 'givenname', 'mail', 'telephonenumber', 'mobile', 'title', 'employeenumber', 'memberof'])...
Debug - ldap_search() Ok.
The LDAP query '(objectClass=inetOrgPerson)' returned 13 elements.
Displaying only 10 elements (use --max-records=xx to change this limit).
------------------------------------------------
LDAP Structure:
Info: when a field is empty on a given record, it is not returned by LDAP.
------------------------------------------------
givenname : bruce
sn        : Lee
uid       : blee
mail      : bruce.lee2@combodo.com
mobile    : 0608080808
------------------------------------------------
givenname : chuck
mail      : chuck.norris@combodo.com
sn        : Norris
uid       : cnorris
------------------------------------------------
```

The first column of the output is the name of the field in LDAP (all fields returned by the LDAP query are listed) and the second column shows the values of the first record found in LDAP. Based on the values displayed you can complete the configuration of the mapping in the configuration file `conf/params.local.xml`.

By default `ldap_test.php` only requests the attributes used in the Person's mapping. To request all the available LDAP attributes, add the parameter `--attributes=*` to the `ldap_test.php` command line

By default `ldap_test.php` dumps only the first 10 records of the results. You can adjust this number to *xx* records by specifying the parameter `--max-records=xx` on the command line.

Finally you can test your configuration **without importing any data in iTop** by running the following command from the command line:

```
php exec.php --console_log_level=9 --collect_only
```

This produces an output similar to the one shown below:

```
Debug - OK, the required PHP version to run this application is 5.3.0. The current PHP version is 7.2.7-0ubuntu0.18.04.2.
Debug - OK, the required extension 'simplexml' is installed (current version: 7.2.7-0ubuntu0.18.04.2 >= 0.1).
Debug - OK, the required extension 'dom' is installed (current version: 20031129 >= 1.0).
Debug - The following configuration files were loaded (in this order):

        1. /opt/dev/ldap-collector/conf/params.distrib.xml
        2. /opt/dev/ldap-collector/collectors/params.distrib.xml
        3. /opt/dev/ldap-collector/conf/params.local.xml

The resulting configuration is:

<?xml version="1.0" encoding="UTF-8"?>
<parameters>
  <itop_url>http://itop-demo/trunk</itop_url>
  <itop_login>admin</itop_login>
  <itop_password>admin</itop_password>
  <console_log_level>6</console_log_level>
  <syslog_log_level>-1</syslog_log_level>
  <max_chunk_size>1000</max_chunk_size>
  <itop_synchro_timeout>600</itop_synchro_timeout>
  <stop_on_synchro_error>no</stop_on_synchro_error>
  <curl_options>
    <CURLOPT_SSLVERSION>CURL_SSLVERSION_SSLv3</CURLOPT_SSLVERSION>
    <CURLOPT_SSL_VERIFYHOST>0</CURLOPT_SSL_VERIFYHOST>
    <CURLOPT_SSL_VERIFYPEER>1</CURLOPT_SSL_VERIFYPEER>
  </curl_options>
  <collect_person_only>no</collect_person_only>
  <ldaphost>192.168.10.13</ldaphost>
  <ldapport>389</ldapport>
  <ldapdn>OU=FGA,DC=combodo,DC=net</ldapdn>
  <ldaplogin>COMBODO\administrateur</ldaplogin>
  <ldappassword>xxxxxx</ldappassword>
  <ldappersonfilter>(objectClass=person)</ldappersonfilter>
  <itop_group_pattern>/^CN=itop-(.*),OU=.*/</itop_group_pattern>
  <person_fields>
    <primary_key>samaccountname</primary_key>
    <name>sn</name>
    <first_name>givenname</first_name>
    <email>mail</email>
    <phone>telephonenumber</phone>
    <mobile_phone>mobile</mobile_phone>
    <function>title</function>
    <employee_number>employeenumber</employee_number>
  </person_fields>
  <person_defaults>
    <org_id>Demo</org_id>
    <status>active</status>
  </person_defaults>
  <ldapuserfilter/>
  <user_id>samaccountname</user_id>
  <user_contactid>mail</user_contactid>
  <synchronize_profiles>no</synchronize_profiles>
  <user_fields>
    <primary_key>samaccountname</primary_key>
    <login>samaccountname</login>
    <contactid>mail</contactid>
  </user_fields>
  <user_defaults>
    <profile>Portal user</profile>
    <language>EN US</language>
  </user_defaults>
  <prefix/>
  <json_placeholders>
    <prefix>$prefix$</prefix>
    <persons_data_table>synchro_data_$prefix$ldap_persons</persons_data_table>
    <users_data_table>synchro_data_$prefix$ldap_users</users_data_table>
  </json_placeholders>
  <ldapfilter>(objectClass=person)</ldapfilter>
</parameters>

Debug - Persons: Mapping of the fields:
   iTop 'primary_key' is filled from LDAP 'samaccountname' 
   iTop 'name' is filled from LDAP 'sn' 
   iTop 'first_name' is filled from LDAP 'givenname' 
   iTop 'email' is filled from LDAP 'mail' 
   iTop 'phone' is filled from LDAP 'telephonenumber' 
   iTop 'mobile_phone' is filled from LDAP 'mobile' 
   iTop 'function' is filled from LDAP 'title' 
   iTop 'employee_number' is filled from LDAP 'employeenumber' 
   iTop 'org_id' is filled with the constant value 'Demo'
   iTop 'status' is filled with the constant value 'active'

Debug - LDAPUsers: Mapping of the fields:
   iTop 'primary_key' is filled from LDAP 'samaccountname' 
   iTop 'login' is filled from LDAP 'samaccountname' 
   iTop 'contactid' is filled from LDAP 'mail' 
   iTop 'language' is filled with the constant value 'EN US'
   iTop 'profile_list' is filled with the constant value 'profileid->name:Portal user'
  
...
```

You can see the order in which the configuration files were loaded and the resulting configuration.

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

The execution of the command line will:

1. Connect to iTop to create the Synchronization Data Sources (or check their definition if they already exist, updating them if needed)
2. Connect to the LDAP server to collect the information about the Persons and the Users
3. Upload the collected data into iTop
4. Synchronize the collected data with the existing iTop Person and Users.

When the collector is run, two Synchro Data Sources are created and used for synchrponizing Person and LDAPUser objects in iTop:![Synchro Data Sources](https://www.itophub.io/wiki/media?w=600&tok=4b1b19&media=extensions%3Aldap-synchro-data-sources.png)

### Scheduling

Once you've run the data collector interactively, the next step is to schedule its execution so that the collection and import occurs automatically at regular intervals.

The data collector does not provide any specific scheduling mechanism, but the simple command line `php exec.php` can be scheduled with either [cron](http://en.wikipedia.org/wiki/Cron) (on Linux systems) or using the [Task Scheduler](http://en.wikipedia.org/wiki/Windows_Task_Scheduler) on Windows.

For optimal results, don't forget to adjust the configuration parameter `full_load_interval` to make it consistent with the frequency of the scheduling.

## Migrating from version 1.1.x to 1.2.x

Between version 1.1.1 and 1.2.0 the structure of the configuration has slightly changed:

- The mapping of the fields between LDAP and iTop is now defined as an array `<person_fields>` for the Person object and `<user_fields>` for the LDAPUser object. The same applies to the default values for the fields which are respectively configured in the arrays `<person_defaults>` and `<user_defaults>`. If you changed the default configuration for these items, you'll have to adjust your configuration file accordingly.
- The parameter `synchro_profils` has been renamed to `synchro_profiles`
- The parameter `synchronize_organization` has been deprecated. If you don't want to synchronize the organizations, don't provide a mapping for the `org_id` field (in `<person_fields>`) and provide a default value for `org_id` in `<person_defaults>`.
- Version 1.1 did not support to run several instances of the collector against the same iTop instance (for multiple LDAP servers), and thus the name of the SQL tables holding the synchro data was using a different scheme. To retain the same name of the SQL data tables, edit the configuration file and put the folling line in the `<json_placeholders>` section:

```
  <json_placeholders>
                <prefix></prefix>
                <persons_data_table>synchro_data_PersonAD</persons_data_table>
                <users_data_table></users_data_table>
        </json_placeholders>
```

## Synchronizing data with several LDAP servers

The current version of the Data collector for LDAP supports only one source LDAP server. However you can run several instances of the collector, each with a different configuration to connect to different LDAP servers but the to the same iTop instance.

In such a configuration, make sure that the `<prefix>` parameter is different for each LDAP server, since each collector needs to create its own set of the Synchro Data Sources in iTop.

### Example

Create two copies of the LDAP data collector: `collector-ldap1` and `collector-ldap2`. In `collector-ldap1/conf/params.local.xml` put:

```
<parameters>
        ...
        <ldaphost>ldap-server1.demo.com</ldaphost>
        <ldapport>389</ldapport>
        <prefix>ldap1_</prefix> <!-- IMPORTANT to have a unique prefix, use only [a-z0-9_] characters -->
</parameters>
```

In `collector-ldap2/conf/params.local.xml` put:

```
<parameters>
        ...
        <ldaphost>ldap-server2.demo.com</ldaphost>
        <ldapport>389</ldapport>
        <prefix>ldap2_</prefix> <!-- IMPORTANT to have a unique prefix, use only [a-z0-9_] characters -->
</parameters>
```

This will create two independent sets of Synchronization Data Sources:![Synchro Data Sources](https://www.itophub.io/wiki/media?w=600&tok=126ee6&media=extensions%3Aldap-multiple-synchro-data-sources.png)