# Predefined response models

- name:

  Predefined response models

- description:

  Pick common answers from a list of predefined replies grouped by categories to update tickets log

- version:

  1.1.4

- release:

  2018-12-19

- itop-version-min:

  2.3.0

- code:

  combodo-predefined-response-models

- diffusion:

  iTop Hub, ITSM Designer

- state:

  stable

- download:

  https://store.itophub.io/en_US/products/combodo-predefined-response-models

- alternate-name:

  Precanned Replies

For iTop versions older than 2.3.0 use a previous version of this component

**Other versions of this component:** [1.0.5](https://www.itophub.io/wiki/page?id=extensions%3Aprecanned-replies-pro_1_0_5)

This extension is a complement to [Send updates by email](https://www.itophub.io/wiki/page?id=extensions%3Aemail_reply). It provides a quick way to fill the case log field by picking from a list of “precanned” answers. The answers are organized into Categories and Organizations (supporting multi-tenancy).

## Features

- List of “precanned” replies, for answering quickly the most common questions
- Organize the answers by category to easily find them
- Support of multi-tenancy: each Organization can have its list of “precanned” answers.
- Attachments can be added to the answer for automatic attachment to the email

## Revision History

| Release Date | Version | Comments                                                     |
| ------------ | ------- | ------------------------------------------------------------ |
| 2018-12-19   | 1.1.4   | Support of JQuery 3 (iTop 2.6.0)                             |
| 2018-06-26   | 1.1.3   | NL translation, default search attributes, iTop 2.5 compatibility |
| 2018-01-26   | 1.1.2   | Add Russian translation.                                     |
| 2016-08-08   | 1.1.1   | Compatibility with iTop 2.3.0 (formatted text) and bug fix to support pagination in the popup dialog for selecting a reply. |
| 2015-09-29   | 1.0.5   | Compatibility with iTop 2.2.0 and custom portals.            |
| 2014-12-10   | 1.0.4   | Cosmetic on the module name (internal).                      |
| 2014-09-25   | 1.0.3   | Better initial sizing and positioning of the dialog box.     |
| 2014-09-15   | 1.0.2   | Handling of the dialog's resize. Localization of the dialog's title. |
| 2014-03-11   | 1.0.1   | Integration of the German translation (thanks to ITOMIG GmbH) |
| 2014-03-06   | 1.0.0   | First released version                                       |

## Limitations

Can be activated only on a single class of object, also it can be an abstract class.

## Requirements

This extension requires the [Send updates by email](https://www.itophub.io/wiki/page?id=extensions%3Aemail_reply) extension to be installed as well.

## Installation & upgrade

- Expand the content of the zip file into the `extensions` folder of iTop

**Compatibility issue**: for iTop version lower than 2.4.0, there is a [special installation/upgrade process](https://www.itophub.io/wiki/page?id=extensions%3Ainstallation#itop_before_240).

- You'll get two folders: `precanned-replies` and `precanned-replies-pro`
- Make sure that the web server process has enough rights to read these folders
- Remove the read-only flag from the iTop configuration file
- Launch the setup by pointing your browser to `http(s)://<itop>/setup`
- When prompted to select the extensions to install, select both “Helpdesk Precanned Replies” and “Helpdesk Precanned Replies - extended for Professionals”

## Configuration

If you have just installed the prerequisite extension [Send updates by email](https://www.itophub.io/wiki/page?id=extensions%3Aemail_reply), you will have to read its [configuration chapter](https://www.itophub.io/wiki/page?id=extensions%3Aemail_reply#configuration). This module has a default configuration that cannot work.

In the iTop configuration file, the administrator defines on which **class** the precanned replies option will be proposed and in which **CaseLog** the reply will be copied.

```
  'precanned-replies' => array (
                'target_class' => 'UserRequest',
                'target_caselog' => 'public_log',
        ),
```

To activate Predefined Requests also on `Incident`, you can use:

```
        'target_class' => 'Ticket',
        'target_caselog' => 'public_log',
```

*Also the field 'public_log' does not exist on Ticket class, it works. When modifying a ticket with no 'public_log', such as a Change or a Problem, it just ignores silently this configuration parameter.*

If you want to add attachments to your Precanned Replies, change the `itop-attachments` section in the iTop configuration file to:

```
        'itop-attachments' => array (
                'allowed_classes' => array (
                          0 => 'Ticket',
                          1 => 'PrecannedReply',
                        ),
                'position' => 'relations',
        ),
```

## Usage

### Creating Precanned Replies

Use the menus under “Service Management” to create and maintain your precanned replies and their categories:

[![Precanned replies menus](https://www.itophub.io/wiki/media?media=extensions%3Aprecanned-replies-menu.png)](https://www.itophub.io/wiki/media-detail?id=extensions%3Aprecanned-replies-pro&media=extensions%3Aprecanned-replies-menu.png)

The form for creating a new Precanned reply looks as follows:

[![New Precanned Reply](https://www.itophub.io/wiki/media?media=extensions%3Aprecanned-replies-new-1-1.png)](https://www.itophub.io/wiki/media-detail?id=extensions%3Aprecanned-replies-pro&media=extensions%3Aprecanned-replies-new-1-1.png)

The “Body” field contains the text that will be added into the case log of the ticket when using this precanned replies. If you have configured the attachments to allow them on Precanned Replies, you can add attachments to the Precanned Reply using the “Attachments” tab.

Within the body of your reply, you can use classic [placeholders](https://www.itophub.io/wiki/page?id=2_6_0%3Aadmin%3Aplaceholders)
`$this->xxxx$` refers to the Ticket in which the predefined response is copied

### Using Precanned Replies

When modifying a Ticket, the public case log contains a new button “Precanned replies…” in its header:

[![Precanned Replies button](https://www.itophub.io/wiki/media?media=extensions%3Aprecanned-replies-button-1-1.png)](https://www.itophub.io/wiki/media-detail?id=extensions%3Aprecanned-replies-pro&media=extensions%3Aprecanned-replies-button-1-1.png)

Click on the “Precanned replies…” button to select a Precanned Reply from the list:[![Select a Precanned Reply](https://www.itophub.io/wiki/media?w=600&tok=a2e310&media=extensions%3Aprecanned-replies-select-answer.png)](https://www.itophub.io/wiki/media-detail?id=extensions%3Aprecanned-replies-pro&media=extensions%3Aprecanned-replies-select-answer.png)

You can use the search criteria at the top to filter the list.

When clicking “Ok”, the answer is written into the case log field. Attachments (if any) to the Precanned reply are added to the answer (the count next to the paper clip icon is increased accordingly):

[![Reply added](https://www.itophub.io/wiki/media?media=extensions%3Aprecanned-replies-done-1-1.png)](https://www.itophub.io/wiki/media-detail?id=extensions%3Aprecanned-replies-pro&media=extensions%3Aprecanned-replies-done-1-1.png)

When submitting the modifications to the ticket, the case log will be updated, as if the answer was typed manually.

The attachments are **only** sent by email: they are **not** added to the ticket.

If the checkbox “Send the reply by email” is checked, an answer will be sent by email, as explained in [Send updates by email](https://www.itophub.io/wiki/page?id=extensions%3Aemail_reply).