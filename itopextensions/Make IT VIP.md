# Make IT VIP

- name:

  Make IT VIP

- description:

  Flag important contacts in your database and highlight tickets

- version:

  1.0.0

- release:

  2019-01-10

- itop-version-min:

  2.3.0

- download:

  https://store.itophub.io/en_US/products/combodo-make-it-vip

- code:

  combodo-make-it-vip

- state:

  stable

Manage VIP User Requests as they deserve to be !

## Features

This extensions allows you to:

- Identify VIP persons in your CMDB
- If a caller is a VIP, all his User Requests will have the priority set to critical.
- The header of the ticket will be highlighted with a VIP icon

## Revision History

| Version | Release Date | Comments      |
| ------- | ------------ | ------------- |
| 1.0.0   | 2019-01-07   | First version |

## Limitations

- Translation available only in English and French
- First version only works with **Simple Ticket Management**.

## Requirements

This extension require the usage of User Request in iTop 2.3.0 or above

## Installation

Use the [Standard installation process](https://www.itophub.io/wiki/page?id=extensions%3Ainstallation) for this extension.

## Configuration

no configuration

## Usage

First this extension change the form for a Person.
A new attribut VIP (yes,no) is define to identify if a person is a VIP.
By default the value is set to no

[![img](https://www.itophub.io/wiki/media?media=extensions%3Amake-it-vip-person.png)](https://www.itophub.io/wiki/media?media=extensions%3Amake-it-vip-person.png)

When a User Request is created the attribut VIP is updated automatically according the value set for the corresponding caller.
This attribut can be used to extract easily VIP User Request for reporting purpose

The priority of the ticket is forced to be critical as soon as the caller is a VIP

The Header of the User Request is highlighted with a vip icon

[![img](https://www.itophub.io/wiki/media?media=extensions%3Amake-it-vip-user-request.png)](https://www.itophub.io/wiki/media?media=extensions%3Amake-it-vip-user-request.png)