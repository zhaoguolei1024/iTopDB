# Data collector for vSphere

- name:

  Data collector for vSphere

- description:

  Collector for vSphere data synchronization in iTop CMDB (VM, Hypervisor, Cluster)

- version:

  1.0.12

- release:

  2020-04-02

- code:

  combodo-data-collector-for-vsphere

- state:

  stable

- alternate-name:

  vSphere Data Collector

- diffusion:

  iTop Hub

This stand-alone application collects information about a whole data center from a vSphere server (using the vSphere Web Services) and synchronizes this information with iTop using several Synchronization Data Sources.

![vSphere Data Collector connections](https://www.itophub.io/wiki/media?w=450&tok=83cef2&media=extensions%3Avsphere-data-collector.png)

## Features

- Automated inventory of Servers (with their Brand, Model), Hypervisors (with their OS Family and OS Version), Farms, Virtual Machines (with their OS Family and OS Version).
- Optional inventory of IPv4 addresses and logical interfaces
- The collector can reside on any system with web access to both vSphere Web Services and iTop.
- Automatic creation and update of the Synchronization Data Sources in iTop.
- Starting with version 1.0.12 the collection mechanism is somehow extensible

This collector makes use of iTop's built-in Data Synchronization mechanism. For more information about how the data synchronization works, refer to [Data Synchronization Overview](https://www.itophub.io/wiki/page?id=latest%3Aadvancedtopics%3Adata_synchro_overview) and relies on [Data collector Base](https://www.itophub.io/wiki/page?id=extensions%3Aitop-data-collector-base) mechanism

## Revision History

| Release Date | Version | Comments                                                     |
| ------------ | ------- | ------------------------------------------------------------ |
| 2020-07-07   | 1.0.13  | - Differenciates error/logs between teemip NOT installed and itop REST API issue - Multi configuration file - New CSV collector - Configurable timestamp added in the logs - New option for usage: –help |
| 2020-04-02   | 1.0.12  | - Made the Server and Hypervisor collectors configurable - Fix for a crash caused by a blank datastore name (thanks to David Wißen from ITOMIG for reporting it). - Fix for some OpenVM Tools reporting IP addresses with a trailing space (thanks to Martin Raenker from ITOMIG). |
| 2018-12-31   | 1.0.11  | Corrects regression introduced by 1.0.10 : - Improved support of iTop 2.4+ (obsolescence flag) - Removed a debug trace - Fix Virtual machines which “connectionState” is not “connected” are skipped |
| 2018-08-24   | 1.0.10  | Handles TeemIp : - Automatically detects if TeemIp (as an iTop module or as a standalone application) is present. - Optional synchronization of IPv4 addresses - Optional synchronisation of logical interfaces |
| 2018-07-02   | 1.0.9   | Robustness : - more traces in debug mode (–console_log_level=9) - skipping virtual machines which “connectionState” is not “connected”, since most of their properties are not accessible and would crash PHP/Soap (with a core dump !!) |
| 2018-02-22   | 1.0.8   | - The `os_version_mapping` was used only for Hypervisors, made it work for VirtualMachines also. Proper support of UTF-8 characters in regular expressions (the code now always uses the `u` modifier) |
| 2017-04-24   | 1.0.7   | Fixed the value for the status of VMs: 'production' instead of 'active'. |
| 2017-03-08   | 1.0.6   | - Code cleanup. - Data Synchro `status` and `full_load_interval` are now homogeneous and configurable parameters for all data sources. - OS Version and OS Family have their own mapping table. - Fix for the Hypervisor status value (now defaults to “production”). - Addition of the `check_soap.php` script for troubleshooting. - Protect against a PHP crash in case of a disconnected ESX. - Do not collect an IPV6 as the management IP address of a virtual machine (since the field can only contain an IPV4). Many thanks to Andrew Armstrong for proposing this fix. |
| 2016-12-08   | 1.0.5   | New options to bypass SSL certificate validation and automatic detection of invalid certificates. |
| 2015-11-16   | 1.0.4   | Replace line-breaks by spaces inside the description of a VM. Fix the +1 on the number of vCPUs |
| 2015-04-17   | 1.0.3   | Added the collection of the “description” field for a VM     |
| 2015-02-23   | 1.0.2   | Servers must be loaded before hypervisors                    |
| 2015-01-07   | 1.0.1   | Beta version                                                 |
| 2014-05-13   | 1.0.0   | First alpha version                                          |

## Limitations

This version of the collector does not collect the Data Stores (they do not exist in the iTop standard data model). Logical interfaces may be collected in the case where TeemIp (module or standalone) is used.

If IP collection is enabled, only IPv4 addresses are collected, not IPv6.

The current version of the collector is designed to collect information from a **single vSphere** server. To collect and reconcile information form several vSphere servers into one iTop, check the section [Collecting from several vSphere servers](https://www.itophub.io/wiki/page?id=extensions%3Avsphere-data-collector#collecting_information_from_several_vsphere_servers) below.

## Requirements

- PHP Version 5.3.0 (support of namespaces is required for the vSphere API library)
- An access to the vSphere web services API
- An access to the iTop web services (REST + synchro_import.php and synchro_exec.php)
- \+ [Data collector Base](https://www.itophub.io/wiki/page?id=extensions%3Aitop-data-collector-base#requirements) requirements.

## Installation

- Expand the content of the zip archive on a folder on the machine that will run the collector application. This machine *must* have a web access to both the vSphere server and the iTop server.
- Edit the content of the file `conf/params.local.xml` to suit your installation, supplying the appropriate credentials to connect to vSphere and iTop.

## Configuration

Create the file `params.local.xml` in the `conf` directory with the following XML content:

```
<?xml version="1.0" encoding="UTF-8"?>
<parameters>
  <itop_url>https://localhost/</itop_url>
  <itop_login>admin</itop_login>
  <itop_password>admin</itop_password>
  <vsphere_uri>192.168.10.12:443</vsphere_uri>
  <vsphere_login>admin</vsphere_login>
  <vsphere_password>admin</vsphere_password>
  <contact_to_notify>john.doe@demo.com</contact_to_notify>
  <synchro_user>admin</synchro_user>
  <default_org_id>Demo</default_org_id>
</parameters>
```

| Parameter                  | Meaning                                                      | Sample value           |
| -------------------------- | ------------------------------------------------------------ | ---------------------- |
| itop_url                   | URL to the iTop Application                                  | https://localhost/itop |
| itop_login                 | Login (user account) for connecting to iTop. Must have admin rights for executing the data synchro. | admin                  |
| itop_password              | Password for the iTop account.                               |                        |
| vsphere_uri                | The address/port to connect to vSphere. Format: <name>:<port> or <ip_address>:<port> | 192.168.10.12:443      |
| vsphere_login              | Login for connecting to vSphere                              | administrateur         |
| vsphere_password           | Password corresponding to the vSphere login                  |                        |
| vsphere_connection_options | List of PHP Stream context options to pass to the VMWarephp library in order to tune the https connection. |                        |
| contact_to_notify          | The email address of an existing contact in iTop, to be notified of the results of the synchronization |                        |
| default_org_id             | The name of the default Organization in which the CIs (Servers, Hypervisors, Farms…) will be created | Demo                   |

### Other optional parameters

| Parameter    | Meaning                                                      | Sample value |
| ------------ | ------------------------------------------------------------ | ------------ |
| synchro_user | If the user account used for running this synchronization is *not* an Administrator, then its login must be specified here, since iTop allows only the administrators and the specified user to run the synchronization. |              |

### Placeholders in the configuration of the data sources

The JSON files used to configure the data sources contain several placeholders initialized from the configuration above (`$contact_to_notify$`), but also additional placeholders specific to the data sources. These placeholders can be configured inside the `<json_placeholders>` tag in the parameters file:

```
<?xml version="1.0" encoding="UTF-8"?>
  <parameters>
    ...
    <json_placeholders type="hash">
      <prefix>vSphere</prefix>
      <full_load_interval>60</full_load_interval>
    </json_placeholders> 
    ...
  </parameters>
```

| Parameter          | Meaning                                                      | Sample value |
| ------------------ | ------------------------------------------------------------ | ------------ |
| full_load_interval | The delay (expressed in seconds) between two complete imports of the data. The objects which have not been detected by the collector during a timespan longer than this interval will be considered as obsolete and marked as such in iTop. Adjust this value depending on the scheduling recurrence. | 604800       |
| prefix             | The prefix for the name of all Synchronization Data Sources in iTop. If you run several instances of the collector (to collect information from several vSphere servers), change this value so that each data source has a unique name | vSphere      |

The file `params.distrib.xml` contains the default values for the parameters. Both files (`params.distrib.xml` and `params.local.xml`) use exactly the same format. But `params.distrib.xml` is considered as the reference and should remain unmodified. Should you need to change the value of a parameter, copy and modify its definition in `params.local.xml`. The values in `params.local.xml` have precedence over the ones in `params.distrib.xml`

To bypass SSL certificate validation (which is needed if your vSphere server runs with the default certificates installed by vSphere) add the folling lines in the `params.local.xml` file:

```
  <vsphere_connection_options>
        <ssl>
                <verify_peer>0</verify_peer>
                <verify_peer_name>0</verify_peer_name>
                <allow_self_signed>1</allow_self_signed>
        </ssl>
  </vsphere_connection_options>
```

### Brands, Models, OS Family and OS Version normalization

The values collected for Brands, Models and OS Family may be very variable because they came from non homogeneous sources (BIOS, operating system…). The data collector contains a simple mechanism to filter / normalize the values via a manual tuning, before importing them into iTop: a simple *mapping table*.

Creating the *Mapping Table* is an iterative process, since the table must be adapted when the collector encounters new values (new machine with a different BIOS, new operating system…)

Mapping tables are defined and maintained in the configuration file `params.local.xml` (you can copy an example definition from `params.distrib.xml` and ajust it at your will). `brand_mapping` is used for filtering the Brand values, `model_mapping` is used for Models, `os_family_mapping` is used for OS Families and `os_version_mapping` is used for OS Versions.

A *mapping table* is simply an *ordered* list of patterns and replacement strings. For each entry in the list, if the supplied value matches the pattern, it is replaced by the replacement string. The patterns are processed from the first one (top of the list) to the last one (bottom of the list). The processing stops after the first successful match.

The format of each entry in the mapping table is:

```
<pattern>/regular_expression/replacement_string</pattern>
```

Where:

- *regular_expression* is a [PCRE regular expression](http://php.net/manual/en/reference.pcre.pattern.syntax.php) to be matched against the input value,
- *replacement_string* is the resulting value if the input value matches the regular expression.
- Note: any character can be use as a delimiter around the regular expression, not only `/`. But the delimiter character can be present neither in the expression itself nor in the replacement string or the result will be undetermined.

The replacement string is the literal value to use, with the exception of placeholders in the form `%1$s`, `%2$s`… The placeholder `%1$s` corresponds to the part of the input string that matches the whole regular expression. Placeholders `%2$s`, `%3$s` corresponds to matching groups (i.e. parentheses) in the regular expression.

Example of a mapping table for the brands:

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
    <pattern>/Hewlett Packard/Hewlett-Packard</pattern>
    <pattern>/Hewlett-Packard/Hewlett-Packard</pattern>
    <pattern>/Dell/Dell</pattern>
    <pattern>/.*/%1$s</pattern>
  </brand_mapping>
```

The result of such a mapping table will be:

- Any brand containing the letters `IBM` (case sensitive) will become exactly `IBM`
- Any brand containing `Hewlett Packard` (case sensitive) will become exactly `Hewlett-Packard` (notice the added dash between Hewlett and Packard)
- Any brand containing `Hewlett-Packard` (case sensitive) will become exactly `Hewlett-Packard`
- Any brand containing the letters `Dell` (case sensitive) will become exactly `Dell`

Make sure that you keep the last (match all) item in the list to avoid loosing some values.

### IPs and logical interfaces collection

The collector automatically detects if TeemIp is present on the remote iTop application (as a module or even as a stand-alone application). Should that be the case, then the following parameters may trigger IP addresses and logical interfaces collection.

```
<?xml version="1.0" encoding="UTF-8"?>
  <parameters>
    ...
    <teemip_options type="hash">
      <collect_ips>yes</collect_ips>
      <default_ip_status>allocated</default_ip_status>
      <manage_ipv6>no</manage_ipv6>
      <manage_logical_interfaces>yes</manage_logical_interfaces>
      </teemip_options>
    ...
  </parameters>
```

| Parameter                 | Meaning                                                      | Sample value |
| ------------------------- | ------------------------------------------------------------ | ------------ |
| collect_ips               | Triggers IP addresses collection                             | yes          |
| default_ip_status         | Satus of newly created IP addresses                          | allocated    |
| manage_ipv6               | Triggers IPv6 collection - not working yet                   | no           |
| manage_logical_interfaces | Triggers logical interfaces collection as well as the addresses / interfaces links | yes          |

At this stage, IPv6 are not collected. This is due to a limitation of the collector base which cannot handle such objects yet.

### Configurable collectors

Starting with version 1.0.12 of the application, *Server* and *Hypervisor* collectors are configurable by adding extra definitions in the XMl parameter file.

This configuration contains two parts:

1. The first part (under the `<json>` tag) allows to alter the definition of the Synchro Data Source (normally fixed by the .json file associated with the collector class). This is useful to synchronise a new field which was not synchronized by default, or to change a reconciliation rule on a field, etc… Any field under the `attribute_list` part of the JSON file can be modified by specifying a new value in the configuration.
2. The second part (the `<source>` tag) defines the way to collect the data for the attribute. This tag must contain a (partial) PHP expression relative to the Hypervisor object (which is actually a [HostSystem](https://pubs.vmware.com/vsphere-50/topic/com.vmware.wssdk.apiref.doc_50/vim.HostSystem.html) in the vSphere model)

Both parts of the configuration can be used independently (one can alter only the JSON or only the collection, or both).

The example below configures the collection of the “Serial Number” on Servers (from the `otherIdentifyingInfo[EnclosureSerialNumberTag]`) and also uses the collected serial number as the reconciliation key between *Hypervisors* and physical *Servers* (the field `server_id`).

- [config.local.xml](https://www.itophub.io/wiki/page?do=export_code&id=extensions%3Avsphere-data-collector&codeblock=6)

  `<?xml version="1.0" encoding="UTF-8"?> <parameters>   ...   <custom_synchro>    <vSphereHypervisorCollector>      <fields>        <server_id>          <source>hardware->systemInfo->otherIdentifyingInfo[EnclosureSerialNumberTag]</source>          <json>            <reconciliation_attcode>serialnumber</reconciliation_attcode>          </json>        </server_id>      </fields>    </vSphereHypervisorCollector>    <vSphereServerCollector>      <fields>        <serialnumber>          <source>hardware->systemInfo->otherIdentifyingInfo[EnclosureSerialNumberTag]</source>        </serialnumber>      </fields>    </vSphereServerCollector>  </custom_synchro>   ...  </parameters>`

The special syntax with brackets in the `<source>` tag is currently only supported on the `otherIdentifyingInfo` property.

## Usage

To launch the data collection and synchronization with iTop, run the following command (from the root directory where the data collector application is installed):

```
php exec.php
```

The following (optional) command line options are available:

| Option                      | Meaning                                                      | default value |
| --------------------------- | ------------------------------------------------------------ | ------------- |
| --console_log_level=<level> | Level of output to the console. From -1 (none) to 9 (debug). | 6 (info)      |
| --collect_only              | Run only the data collection, but do not synchronize the data with iTop | false         |
| --synchro_only              | Synchronizes the data previously collected (stored in the `data` directory) with iTop. Do not run the collection. | false         |
| --configure_only            | Check (and update if necessary) the synchronization data sources in iTop and exit. Do NOT run the collection or the synchronization |               |
| --max_chunk_size=<size>     | Maximum number of items to process in one pass, for preserving the memory of the system. If there are more items to process, the application will iterate. | 1000          |

The execution of the command line will:

1. Connect to iTop to create the Synchronization Data Sources (or check their definition if they already exist, updating them if needed)
2. Connect to vSphere to collect the information about the Hypervisors, Farms, Virtual Machines
3. Upload the collected data into iTop
4. Synchronize the collected data with the existing iTop CIs.

### Troubleshooting

If you have troubles connecting to the vSphere server, try the following troubleshooting steps:

1. Check that the connection from the system running PHP to the vSphere server is actually possible. Use a command line tool like `wget` to connect to the vSphere server. For example if your `vsphere_uri` is `192.168.10.12:443`, try:

   ```
   wget --no-check-certificate -O - https://192.168.10.12:443
   ```

   If the connection does not succeed, there may be a firewall blocking your requests, or that vSphere is condifured to operate on a different port (for example `9443`)… ask your IT department about it.

2. Once the connection seem to go fine, configure the proper `vsphere_uri` value in `conf/params.local.xml` and, from the command line (in the `collectors` subdirectory) launch:

   ```
   php check_soap.php
   ```

   The expected output (with `vsphere_uri` = `192.168.10.12:443`) is:

   ```
   Connecting to https://192.168.10.12:443/sdk
   
   Ok, the response looks like a valid SOAP response.
   
   --------------------- DEBUG ----------------
   The request returned:
   <?xml version="1.0" encoding="UTF-8"?>
   <soapenv:Envelope xmlns:soapenc="http://schemas.xmlsoap.org/soap/encoding/"
    xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/"
    xmlns:xsd="http://www.w3.org/2001/XMLSchema"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
   <soapenv:Body>
   <RetrieveServiceContentResponse xmlns="urn:vim25"><returnval><rootFolder type="Folder">group-d1</rootFolder><propertyCollector type="PropertyCollector">propertyCollector</propertyCollector><viewManager type="ViewManager">ViewManager</viewManager><about><name>VMware vCenter Server</name><fullName>VMware vCenter Server 4.1.0 build-345043</fullName><vendor>VMware, Inc.</vendor><version>4.1.0</version><build>345043</build><localeVersion>INTL</localeVersion><localeBuild>0</localeBuild><osType>win32-x86</osType><productLineId>vpx</productLineId><apiType>VirtualCenter</apiType><apiVersion>4.1</apiVersion></about><setting type="OptionManager">VpxSettings</setting><userDirectory type="UserDirectory">UserDirectory</userDirectory><sessionManager type="SessionManager">SessionManager</sessionManager><authorizationManager type="AuthorizationManager">AuthorizationManager</authorizationManager><perfManager type="PerformanceManager">PerfMgr</perfManager><scheduledTaskManager type="ScheduledTaskManager">ScheduledTaskManager</scheduledTaskManager><alarmManager type="AlarmManager">AlarmManager</alarmManager><eventManager type="EventManager">EventManager</eventManager><taskManager type="TaskManager">TaskManager</taskManager><extensionManager type="ExtensionManager">ExtensionManager</extensionManager><customizationSpecManager type="CustomizationSpecManager">CustomizationSpecManager</customizationSpecManager><customFieldsManager type="CustomFieldsManager">CustomFieldsManager</customFieldsManager><diagnosticManager type="DiagnosticManager">DiagMgr</diagnosticManager><licenseManager type="LicenseManager">LicenseManager</licenseManager><searchIndex type="SearchIndex">SearchIndex</searchIndex><fileManager type="FileManager">FileManager</fileManager><virtualDiskManager type="VirtualDiskManager">VirtualDiskManager</virtualDiskManager></returnval></RetrieveServiceContentResponse>
   </soapenv:Body>
   </soapenv:Envelope>
   ---------------------------------------------
   ```

   If the result is not the expected one, check that your vSphere server is properly configured to run as HTTPS (which should be the default).

### Scheduling

Once you've run the data collector interactively, the next step is to schedule its execution so that the collection and import occurs automatically at regular intervals.

The data collector does not provide any specific scheduling mechanism, but the simple command line `php exec.php` can be scheduled with either [cron](http://en.wikipedia.org/wiki/Cron) (on Linux systems) or using the [Task Scheduler](http://en.wikipedia.org/wiki/Windows_Task_Scheduler) on Windows.

For optimal results, don't forget to adjust the configuration parameter `full_load_interval` in the (`json_placeholders` section) to make it consistent with the frequency of the scheduling.

## Data Collection Reference

### Servers and Hypervisors

In the vSphere web services SDK, Hypervisors and physical Servers are represented by the same object [HostSystem](https://code.vmware.com/apis/196/vsphere/doc/vim.HostSystem.html).

The information from the vSphere HostSystem object is imported in iTop into the Server object using the following mapping:

| Field in iTop   | Source in vSphere                                            |
| --------------- | ------------------------------------------------------------ |
| name            | `HostSystem → name`                                          |
| org_id          | Constant value, supplied by the configuration file           |
| brand_id        | The information from `HostSystem → hardware → systemInfo → vendor` is processed through the mapping table named `brand_mapping` |
| model_id        | The information from `HostSystem → hardware → systemInfo → model` is processed through the mapping table named `model_mapping` |
| cpu             | `HostSystem → hardware → cpuInfo → numCpuPackages`           |
| ram             | `HostSystem → hardware → memorySize` divided by (1024*1024)  |
| osfamily_id     | The information from `HostSystem → config → product → name` is processed through the mapping table named `os_family_mapping` |
| osversion_id    | The information from `HostSystem → config → product → fullName` is processed through the mapping table named `os_version_mapping` |
| status          | Constant value: `active`                                     |
| managementip_id | Foreign key to an IPAddress object, if IP collection is activated |

The information from the vSphere HostSystem object is imported in iTop into the Hypervisor object using the following mapping:

| Field in iTop | Source in vSphere                                  |
| ------------- | -------------------------------------------------- |
| name          | `HostSystem → name`                                |
| org_id        | Constant value, supplied by the configuration file |
| server_id     | `HostSystem → name`                                |

The example used in the section [Configurable Collectors](https://www.itophub.io/wiki/page?id=extensions%3Avsphere-data-collector#configurable_collectors) shows how to collect the serial number of servers. Be aware that the information available in the property `otherIdentifyingInfo` seem to depend on the hardware manufacturer and/or the version of the hypervisor. Test on your systems before putting such a modification in production.

### Farms

In the vSphere web services SDK, a Farm is represented by the object [ClusterComputeResource](https://code.vmware.com/apis/196/vsphere/doc/vim.ClusterComputeResource.html).

The information from the vSphere ClusterComputeResource object is imported in iTop into the Farm object using the following mapping:

| Field in iTop | Source in vSphere                                  |
| ------------- | -------------------------------------------------- |
| name          | `ClusterComputeResource → name`                    |
| org_id        | Constant value, supplied by the configuration file |

The list of hypervisors belonging to a farm is collected via the property: ClusterComputeResource → host → name.

### Virtual Machines

In the vSphere web services SDK, a Virtual Machine is represented by the object [VirtualMachine](https://code.vmware.com/apis/196/vsphere/doc/vim.VirtualMachine.html). The information from the vSphere VirtualMachine object is imported in iTop into the VirtualMachine object using the following mapping:

| Field in iTop                                  | Source in vSphere                                            |
| ---------------------------------------------- | ------------------------------------------------------------ |
| name                                           | `VirtualMachine → name`                                      |
| org_id                                         | Constant value, supplied by the configuration file           |
| description                                    | `VirtualMachine → config → annotation`                       |
| cpu                                            | `VirtualMachine → config → hardware → numCPU`                |
| ram                                            | `VirtualMachine → config → hardware → memoryMB`              |
| virtualhost_id                                 | either the Farm (if not empty) or `VirtualMachine → runtime → host → name` |
| If TeemIp is **NOT** used                      |                                                              |
| managementip                                   | `VirtualMachine → guest → ipAddress`                         |
| If TeemIp **IS** used and if IPs are collected |                                                              |
| managementip_id                                | Foreign key to an IPAddress object with ip set to `VirtualMachine → guest → ipAddress` |

### IPv4 Addresses

If enabled (TeemIp required), the information from the vSphere IPv4 addresses is imported in iTop into the IPv4Address object using the following mapping:

| Field in iTop | Source in vSphere                                            |
| ------------- | ------------------------------------------------------------ |
| org_id        | Constant value, supplied by the configuration file           |
| status        | Constant value, supplied by the configuration file           |
| short_name    | `VirtualMachine → guest → hostName`                          |
| ip            | Virtual Machine: `VirtualMachine → guest → ipAddress` Hypervisor: `HostSystem → name` |

### Logical Interfaces

If enabled (TeemIp required), the collector may register the logical interfaces attached to virtual machines. These are imported in iTop into the LogicalInterface objects using the following mapping:

| Field in iTop     | Source in vSphere                                            |
| ----------------- | ------------------------------------------------------------ |
| macaddress        | `VirtualMachine → guest → net → macAddress`                  |
| name              | `VirtualMachine → config → hardware → device → backing →` * `network → name` or * `opaqueNetworkId` or * `deviceName` or * `port` |
| virtualmachine_id | `VirtualMachine → name`                                      |
| ip_list           | List of IP addresses attached to the interface               |

The ip_list attribute is synchronized through the dedicated synchro data source vSphere:lnkIPInterfaceToIPAddress.

## Collecting information from several vSphere servers

Although the current version of the collector supports only the connection to one single vSphere server, it is possible to collect data from several vSphere instances and feed the result into one iTop instance. Here is how to proceed:

- Copy the whole directory containing the collector application, one copy per vSphere server
- Change the configuration file `conf/local.params.xml` in each copy of the collector application to:
  1. provide the proper connection information and credentials to the vSphere server
  2. **important:** set a unique `prefix` (in the configuration file, see [Placeholders above in the configuration file](https://www.itophub.io/wiki/page?id=extensions%3Avsphere-data-collector#placeholders_in_the_configuration_of_the_data_sources)) for each vSphere server
- When the collector is run, this will create (update & execute) a complete set of Data Synchronization sources for each specific vSphere server.
- Schedule the execution of the different collectors at different times to avoid overloading your iTop server by concurrent data synchronizations.

For advanced users: actually there is no need to completely clone the whole collector application for each vSphere server. What really need to be unique for each server is: the configuration file (`conf/params.local.xml`) and the `data` directory. All the other files can be symbolic links to their original version.

You may also be interested by the extension [Synchro Dashboard](https://www.itophub.io/wiki/page?id=extensions%3Aitop-synchro-dashboard) which provides a consolidated dashboard about the status of all the data synchronisation sources on a given iTop instance