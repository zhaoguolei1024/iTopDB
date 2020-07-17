# Database Maintenance Tools

- name:

  Database Maintenance Tools

- description:

  Small tools to detect database incoherences and propose fixes

- version:

  1.0.7

- release:

  2019-03-26

- code:

  combodo-db-tools

- state:

  stable

- download:

  https://store.itophub.io/en_US/products/combodo-db-tools

Database maintenance tools

## Features

Tools for database maintenance.

- Database Info (size)
- Database inconsistency check
- Lost or misplaced attachments (from email to ticket automation)

## Revision history

| Date       | Version | Description                                                  |
| ---------- | ------- | ------------------------------------------------------------ |
| 2010-03-19 | 1.0.7   | Fix typo in German translation                               |
| 2019-01-03 | 1.0.6   | Fix bad server response for reports                          |
| 2018-12-19 | 1.0.5   | - Fix file not found error in reports - Check uniqueness rules - add missing <label> for checkboxes in the UI |
| 2018-06-27 | 1.0.4   | Add DE translation                                           |
| 2018-06-26 | 1.0.3   | Fix label typo                                               |
| 2018-04-11 | 1.0.0   | First stable revision                                        |
| 2018-02-23 | 0.0.12  | Enable 2.5.0 menu overriding capabilities. Add Database info (size) tab. |
| 2018-01-26 | 0.0.9   | Analysis can be done on one class only                       |
| 2018-01-22 | 0.0.5   | The display of the IDs is optional                           |
| 2017-12-14 | 0.0.4   | Database consistency check                                   |

## Usage

Adds a new menu entry in the Admin Menu : **DB Tools**

[![img](https://www.itophub.io/wiki/media?w=600&tok=d9c583&media=extensions%3Ascreenshot-localhost-2018-01-22-13-52-52.png)](https://www.itophub.io/wiki/media-detail?id=extensions%3Acombodo-db-tools&media=extensions%3Ascreenshot-localhost-2018-01-22-13-52-52.png)

#### Database Information

The size of the database is displayed.

#### Database inconsistencies

Various display mode are available:

##### Errors

Display only database inconsistencies.

##### Errors and values

Corresponding field values are displayed.

##### Errors and Id list

Generate a list of IDs in order to generate an SQL SELECT

##### Report

Generate all the inconsistencies and allow the user to download the result as a zipped file.

#### Lost attachments

Here you can search your database for lost or misplaced attachments. This is NOT a data recovery tool, is does not retrieve deleted data.