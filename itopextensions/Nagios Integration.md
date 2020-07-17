# Nagios Integration

- name:

  itop-nagios-integration

- version:

  1.0.0

- release:

  2016-09-27

- description:

  Integration of a Nagios page in iTop and tickets creation from Nagios

- itop-version:

  2.0

- keyword:

  [nagios](https://www.itophub.io/wiki/page?id=keyword&dataflt[0]=keyword_%3Dnagios), [monitoring](https://www.itophub.io/wiki/page?id=keyword&dataflt[0]=keyword_%3Dmonitoring)

- dependencies:

  itop-config-mgmt

- author:

  Combodo

- download:

  http://www.combodo.com/itop-extensions/itop-nagios-integration-1.0.0-173.zip

Very old extension, using out of date technics…

This page describes two topics:

1. A small iTop extension to display (in a separate tab “Monitoring”) the monitoring status of a device in production (taken from an external monitoring system like Nagios, CheckMK, Zabbix, Shinken…).
2. A simple command line script to create an incident ticket in iTop from a monitoring system

# Monitoring Tab in iTop

## Features

Display an additional tab “Monitoring”, containing an IFRAME to the status of the device in the monitoring system (Nagios or equivalent). This extra tab is automatically displayed on all devices in production.

## Revision History

| Version | Release Date | Comments      |
| ------- | ------------ | ------------- |
| 1.0.0   | 2016-09-23   | First version |

## Limitations

Because of the browser's security rules, the content of the Monitoring iframe will **not** display at all in iTop if either:

- iTop uses an `https` (secure) connection whereas the pages from the monitoring application are served in `http` (non-secure), or
- the Nagios web server populates the HTTP `X-Frame-Options` header with either `DENY` or `SAMEORIGIN` (refer to [X-Frame-Options definition](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Frame-Options) for more information)

The integration does not take care of the authentication to the Monitoring system. Depending on the configuration of your monitoring system, you may need to authenticate in order to see the content of the “Monitoring” tab.

## Requirements

You must have an up and running monitoring system providing a status web page, per device, accessible via a “direct” URL with the name (or the IP address) of the monitored device as a parameter in the URL.

## Installation

Put the content of the downloaded `.zip` into the `extensions` folder (check the rights !) and run the setup again to pick the new extension for installation.

## Configuration

This module has only two parameters `nagios_url` and `target_classes`.

| Parameter      | Type   | Usage                                                        | Default value                                                |
| -------------- | ------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| nagios_url     | String | URL to display the nagios status web page for the device. The placeholder `$this->name$` in the URL is replaced by name of the CI. | `https://nagios_server/cgi-bin/status.cgi?host=$this->name$` |
| target_classes | Array  | A list of classes for which to display the “Monitoring” tab. Child classes of the specificed classes also inherit the tab. | `array('ConnectableCI')`                                     |

The `target_classes` must be classes derived from `FunctionalCI`, since the code looks for the `status` of the CI.

### Example

The following configuration:

```
        'itop-nagios-integration' => array (
                'nagios_url' => 'https://mynagios.mycompany.com/cgi-bin/status.cgi?host=$this->name$',
        ),
```

Will display the page at the location `https://mynagios.mycompany.com/cgi-bin/status.cgi?host=server4.demo.com` as an extra tab “Moniting” in the details of the Server `server4.demo.com`.

## Usage

Navigate to a device in production (status == production) to see the extra “Monitoring” tab in the details of the device.

The “Monitoring” tab is **not** displayed when editing the properties of the device, since there is nothing to modify inside this tab.

# Creating a ticket from the Nagios server

1. Pick the [create-ticket-script](https://www.itophub.io/wiki/page?id=latest%3Aadvancedtopics%3Acreate_ticket) script in your favorite scripting language and install its dependencies on the Nagios server
2. Copy this script in <yourDirectory> on the Nagios server. Don't forget to adjust the rights and mark the script as executable (`chmod +x <create-ticket-script>`)
3. Define a new Nagios command by adding following to your Nagios command file (most of the time it is called `commands.cfg`)

```
# Create incident tickets in iTop command definition 
define command{ 
        command_name    create-iTop-ticket 
        command_line    <yourDirectory>/<create-ticket-script> \"$HOSTNAME$\" \"$SERVICEDESC$\" \"$SERVICESTATE$\" \"$SERVICESTATETYPE$\"
```

where `<your_directory>` is the path where you copied the script and <create-ticket-script> is either `create-ticket.php`, `create-ticket.py`, `create-ticket.pl` or `create-ticket.bash`.

Step 4: Use this command in an event handler option for each host or service template that should trigger a ticket creation:

You can define it globally for all hosts and services using following options defined most of the time in nagios.cfg:

```
global_host_event_handler=create-iTop-ticket
global_service_event_handler= create-iTop-ticket
```

Or for each host and services using following options:

```
event_handler   create-iTop-ticket
event_handler_enabled  1
```

if you choose the latter option, you will have to configure the handler for each host and service templates you create.

Once done, next time you will have a HARD alarm in Nagios it will create a ticket automatically in iTop !