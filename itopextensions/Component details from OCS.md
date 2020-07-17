# Component details from OCS

- name:

  Component details from OCS

- description:

  Display OCS screen within iTop object, such as Server, PC and Virtual Machine

- version:

  1.0.4

- release:

  2018-09-04

- itop-version-min:

  2.0

- download:

  http://www.combodo.com/itop-extensions/xxxx.zip

- state:

  Stable

## Features

This extension is a complement to the extension [Data collector for OCS Inventory](https://www.itophub.io/wiki/page?id=extensions%3Aocsng-data-collector) which collects information from a [OCS Inventory NG](https://www.ocsinventory-ng.org/) server.

This additional (and optional) extension displays the content of the OCS Inventory pages directly inside iTop, for each synchronized object (Server, PC or Virtual Machine): within a tab containing the OCS page for the device (using an IFRAME).

[![img](https://www.itophub.io/wiki/media?w=650&tok=59d59a&media=extensions%3Aocsngitopframe.png)](https://www.itophub.io/wiki/media?media=extensions%3Aocsngitopframe.png)

## Revision History

| Date       | Version | Description                                                  |
| ---------- | ------- | ------------------------------------------------------------ |
| 2018-09-04 | 1.0.4   | First public version. No longer requires an alteration of the data model. |

## Limitations

## Requirements

- PHP Version 5.3.0
- The extension [Data collector for OCS Inventory](https://www.itophub.io/wiki/page?id=extensions%3Aocsng-data-collector) installed and working on your iTop

## Installation

#### Automated installation via iTop Hub

- Go to the [extensions store](https://store.itophub.io/en_US/products/itop-ocsng) on iTop Hub
- Click on the cart icon to make the acquisition of the extension and follow the on-screen instructions to deploy it on your iTop instance

#### Manual installation

- unzip the file “itop-ocsng.zip” into the iTop `extensions` folder
- make sure that the web server process has enough rights to read the copied files
- Launch iTop setup
- Select the OCS Inventory Integration extension, when prompted

[![img](https://www.itophub.io/wiki/media?w=450&tok=fbdec2&media=extensions%3Aocsngextensionsetup.png)](https://www.itophub.io/wiki/media?media=extensions%3Aocsngextensionsetup.png)

## Configuration

- Edit the iTop configuration file to specify the URL to access the OCS web server:

```
      'itop-ocsng' => array (
                'ocsng_url' => 'http://localhost/ocsreports/',
        ),
```

## Usage

[![img](https://www.itophub.io/wiki/media?w=650&tok=59d59a&media=extensions%3Aocsngitopframe.png)](https://www.itophub.io/wiki/media?media=extensions%3Aocsngitopframe.png)