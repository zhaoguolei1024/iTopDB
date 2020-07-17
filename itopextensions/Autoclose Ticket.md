# Autoclose Ticket

- name:

  Autoclose Ticket

- description:

  Auto close resolved User Request and Incident tickets

- version:

  1.0.1

- release:

  2016-08-10

- itop-version-min:

  2.0.2

- download:

  https://store.itophub.io/en_US/products/combodo-autoclose-ticket

- code:

  combodo-autoclose-ticket

This page describes how the extension combodo auto close allows iTop to automatically close resolved User Request and Incident after a configured delay.

## Features

This extension adds a new background process handled by cron.php to automatically close User Request and Incident according to the autoclosure delay defined in the iTop configuration file.

## Limitations

This extension is not handling Change and Problem tickets.

## Requirements

No requirement

## Revision history

| Date       | Version | Description                                                  |
| ---------- | ------- | ------------------------------------------------------------ |
| 2016-08-10 | 1.0.1   | Performance optimization: do not load all the columns of the tickets in the query. |
| 2014-03-04 | 1.0.0   | First release                                                |

## Installation

1. Download the package: [autoclose-ticket-1.0.1-164.zip](http://www.combodo.com/itop-extensions/autoclose-ticket-1.0.1-164.zip) and expand the folder “combodo-autoclose-ticket” into the “**extensions**” directory of iTop.
2. If you have already installed iTop make sure that the configuration file `config-itop` in `conf/production` is NOT read-only.
3. Point your web browser to `http(s)://<your_itop_root>/setup` and follow the wizard. Make sure that you select the option to “Upgrade an existing iTop instance”:
4. 

[![img](https://www.itophub.io/wiki/media?w=300&tok=c529d3&media=extensions%3Aemail-upgrade-screenshot1.png)](https://www.itophub.io/wiki/media?media=extensions%3Aemail-upgrade-screenshot1.png)

[![img](https://www.itophub.io/wiki/media?w=300&tok=2a82a7&media=extensions%3Aemail-upgrade-screenshot2.png)](https://www.itophub.io/wiki/media?media=extensions%3Aemail-upgrade-screenshot2.png)

Finally check the module “Auto closure of Incident and User Request” in the list of extensions at the end of the interactive wizard. Then complete the installation.

[![img](https://www.itophub.io/wiki/media?w=300&tok=6ef9db&media=extensions%3Acombodo-autoclose-ticket-screnshot1.png)](https://www.itophub.io/wiki/media-detail?id=extensions%3Aauto_close_request&media=extensions%3Acombodo-autoclose-ticket-screnshot1.png)

## Configuration

Once the new module has been installed, edit the configuration file config-itop.php and look for the following new section:

```
        'combodo-autoclose-ticket' => array (
                'incident_autoclose_delay' => '7',
                'userrequest_autoclose_delay' => '7',
        ),
```

This section allows you to define the value for the auto closure delay for incident and user request.

Delays are given in *days*. By default, incident and user request are closed automatically after 7 days.

The automatic closure of the incidents and the user requests is handled by the service cron.php once a day. Make sure this one is scheduled to run on your system. More information in the chapter about [Background tasks](https://www.itophub.io/wiki/page?id=2_3_0%3Aadmin%3Acron).

To check the status of this service, use the command:

```
php webservice/cron.php --auth_user=user --auth_pwd=password --status_only=1
```

[![img](https://www.itophub.io/wiki/media?w=600&tok=d1758e&media=extensions%3Acombodo-autoclose-ticket-screnshot2.png)](https://www.itophub.io/wiki/media-detail?id=extensions%3Aauto_close_request&media=extensions%3Acombodo-autoclose-ticket-screnshot2.png)

The task *AutoCloseTicket* will not be listed here if the CRON has not **run at least once** since the extension has been installed.

## Usage

When a user request or an incident is closed automatically, the user satisfaction is set to the default value defined in the data model: “Very satisfied”