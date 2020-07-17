# Dispatch Incident to team

- name:

  Dispatch Incident to team

- description:

  Dispatch an incident to a team without assigning an agent

- version:

  1.1.6

- release:

  2018-12-19

- itop-version-min:

  2.1.0

- code:

  combodo-dispatch-incident

- diffusion:

  iTop Hub, ITSM Designer

- state:

  stable

- download:

  https://store.itophub.io/en_US/products/combodo-dispatch-incident

- alternate-name:

  Dispatch Incident

For iTop versions older than 2.1.0 use a previous version of this component, for iTop 2.1.0 or newer use this version of the component.

**Other versions of this component:** [1.0.2](https://www.itophub.io/wiki/page?id=extensions%3Acombodo_dispatch_incident_1_0)

The standard life cycle for Incident tickets in iTop does not allow to assign a ticket to a Team without assigning it to a specific Person inside this Team. By creating a new state *dispatched*, this extension allows to *dispatch* an Incident ticket to a Team, without assigning it to particular Person. From the *dispatched* state the Incident can then be assigned to a Person.

## Features

Dispatch an Incident to a Team before assigning it to a Person.

The standard Incident life-cycle is the following:

[![Standard Incident Life-cycle](https://www.itophub.io/wiki/media?w=600&tok=07afb5&media=extensions%3Aincident-std-lifecycle.png)](https://www.itophub.io/wiki/media-detail?id=extensions%3Acombodo_dispatch_incident&media=extensions%3Aincident-std-lifecycle.png)

Once the extension has been installed, the Incident life-cycle becomes as follows:

[![Incident Life-cycle with "dispatched" state](https://www.itophub.io/wiki/media?w=600&tok=af5085&media=extensions%3Aincident-modified-lifecycle.png)](https://www.itophub.io/wiki/media-detail?id=extensions%3Acombodo_dispatch_incident&media=extensions%3Aincident-modified-lifecycle.png)

The definition of the TTO (Time To Own) metric is also modified to take into account the “dispatched” state (The Time To Own stops when the ticket is actually assigned to a Person, not only dispatched to a Team).

Actually two new states are added to the life-cycle: *dispatched* and *redispatched*, to take into account the first assignment of a ticket. When a ticket which was assigned to a Person is dispatched again to a Team, the agent to which the ticket was assigned is cleared (even if the ticket is dispatched again to the same team).

## Revision History

| Release Date | Version | Comment                                                      |
| ------------ | ------- | ------------------------------------------------------------ |
| 2018-12-19   | 1.1.6   | NL and ES translations                                       |
| 2018-07-02   | 1.1.4   | ES and DE translations                                       |
| 2018-01-26   | 1.1.3   | Revision of the Russian dictionnary.                         |
| 2017-11-14   | 1.1.2   | Revision of the German dictionnary.                          |
| 2014-11-19   | 1.1.1   | Adapted to iTop > 2.1.0, which gives more flexibility for developing other modules that could add states to the tickets |
| 2014-03-11   | 1.0.2   | Integration of the German translation (thanks to ITOMIG GmbH) |
| 2014-02-28   | 1.0.0   | First version                                                |

## Installation

1. Expand the zip file of the extension and copy the folder `combodo-dispatch-incident` into the `extensions` folder of iTop, and make sure that the folder can be read by the web server process.
2. If iTop is already installed, make sure that the configuration file is not read-only
3. Launch the setup program by pointing your browser to http://<itop>/setup/
4. When prompted to select the extensions to install, check “Dispatch of Incidents” and complete the setup.

[![Installation screen](https://www.itophub.io/wiki/media?w=450&tok=9f5575&media=extensions%3Adispatch-incident-install.png)](https://www.itophub.io/wiki/media-detail?id=extensions%3Acombodo_dispatch_incident&media=extensions%3Adispatch-incident-install.png)

## Configuration

This extension has no specific configuration setting.

## Usage

The new *dispatched* state is fully integrated with the life-cycle of the ticket. For example, when creating a new Incident, an extra button “Dispatch to a team” appears: [![New button "Dispatch to a team"](https://www.itophub.io/wiki/media?w=600&tok=20ac02&media=extensions%3Adispatch-incident-new-button.png)](https://www.itophub.io/wiki/media-detail?id=extensions%3Acombodo_dispatch_incident&media=extensions%3Adispatch-incident-new-button.png)

On an Incident in state *new*, the action “Dispatch to a team..” is available in the drop-down list of actions. [![New action "Dispatch to a team"](https://www.itophub.io/wiki/media?media=extensions%3Adispatch-incident-popup-menu.png)](https://www.itophub.io/wiki/media-detail?id=extensions%3Acombodo_dispatch_incident&media=extensions%3Adispatch-incident-popup-menu.png)

A user must have either the profile “Service Desk Agent” or “Support Agent” (or Administrator) to be allowed to dispatch a ticket.

The list of teams to which the ticket can be dispatched are the same as the ones used when assigning the ticket directly to a Team and a Person. The possible Teams are defined by the Delivery Model of the Organization of the ticket.