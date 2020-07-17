# Communications to the Customers

- name:

  Communications to the Customers

- description:

  Communications to the Customers via the portal

- version:

  1.1.0

- release:

  2020-02-03

- itop-version-min:

  2.4.0

- code:

  itop-communications

- state:

  stable

- diffusion:

  iTop Hub

Create and publish customer oriented communications to be displayed on the user portal.

For iTop 2.3.2 to 2.3.4, use v1.0.10 as support for iTop 2.3.x was dropped in v1.1.0.

## Features

- Create text based or image based communications (formatting including hyperlinks is supported)
- Quick formatting: title / description / predefined icon
- Communications are active for a predefined time-frame (i.e. they have a predefined start and end date)
- Communications can be delivered to users from selected organizations only

## Revision history

| Date       | Version | Description                                                  |
| ---------- | ------- | ------------------------------------------------------------ |
| 2020-02-03 | 1.1.0   | * Add compatibility with iTop 2.7+ * Add MySQL8 compatibility * Minimum iTop version set to 2.4.0 |
| 2019-09-11 | 1.0.10  | * Update extension description * Correctly display and hide communications to user with silos |
| 2018-12-19 | 1.0.9   | Update translations                                          |
| 2018-06-27 | 1.0.7   | Add DE translations                                          |
| 2018-06-26 | 1.0.6   | Fix portal tile UI                                           |
| 2016-08-23 | 1.0.5   | Bug fix: the option “cascade to child organizations” was not working |
| 2016-08-08 | 1.0.3   | First released version                                       |

## Limitations

The Wiki syntax (in the text of the communication) creates hyperlinks which point to the console!

## Requirements

iTop 2.3.2 and the new portal.

## Installation

As any other extension:

1. Expand the content of the zip file in the `extensions` folder
2. Make sure that the web server has enough rights to read unzipped files
3. Remove the read-only flag on the iTop configuration file
4. Run the setup by pointing your web browser to `http://<itop>/setup`
5. When prompted, make sure that you select **Communications to the Customers** from the list of extensions to install
6. Complete the installation by clicking “Install!”.

## Configuration

This extensions has no configuration parameter.

## Usage

To create a new *Communication* or to view the list of Communications, click on the menu “Communications” under “Service Management”.

![ "Communications" menu ](https://www.itophub.io/wiki/media?media=extensions%3Acommunications-menu.png)

The menu lists all the “on-going” communications. To see the “closed” communications, open the search form at the top of the page, adjust the search criteria and press the “Search” button.

### Creating a new communication

The form to create a new communication is the following:

![ New Communication form ](https://www.itophub.io/wiki/media?media=extensions%3Acommunications-new.png)

| Field                 | Meaning                                                      |
| --------------------- | ------------------------------------------------------------ |
| Announcer             | The organization owning this communication.                  |
| Status                | Automatically computed based on the start and end dates      |
| Start date            | The date (and time) at which to start showing this communication in the portal |
| End date              | The date (and time) at which to stop showing this communication in the portal |
| Target organizations… | How to interpret the list of “Target organizations”. If the value is `Only the selected ones` the list is an explicit list of all organizations for which to show the communication. If the value is `Cascade to child organizations`, the child organizations of the “Target organizations” will also see the message. |
| Icon                  | An optional icon to display next to the communication in the portal. Choose “None” for displaying no icon. |
| Title                 | An optional plain text title for the communication.          |
| Message               | The actual body of the communication. Use the formatting toolbar to style the text, to insert images or add hyperlinks. |

The end users do not need to have access to the announcer organization in order to view the communications in the portal. The system automatically displays the appropriate communications independently of the usual access rights.

To create a “graphic only” communication (for example a graphic banner), use the “description” field to insert a large version of the banner as either a JPEG or PNG image, leave the title blank and select Icon: “None”. The banner image will be displayed using the complete width for the browser, automatically adjusting to browser resizes.

If no “Target Organizations” is selected, everybody will see the communication

### Display of the communications in the Portal

![ Communications in the portal ](https://www.itophub.io/wiki/media?media=extensions%3Acommunications-portal.png)

When a communication is “on going”, it is displayed in the portal, at the top of the home page. The text of the communications are truncated in order to preserve a constant height for the communications area in the home page.

The user can click on a communication to display it in a popup dialog. This is especially useful on small screens (mobile phones) where the communication may be truncated.

![ Popup showing a communication ](https://www.itophub.io/wiki/media?media=extensions%3Acommunications-popup.png)

If there are several on-going communications at the same time, they are displayed one after the other, using a carousel, automatically sliding to the next communication after 5 seconds. Small bullets are displayed at the bottom of the carousel to allow direct access to the Nth communication. The carousel automatically stops sliding when the user positions the mouse hover it.

When there is no on-going communication, nothing is shown in the home page of the portal.