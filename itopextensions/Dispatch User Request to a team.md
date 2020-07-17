# Dispatch User Request to a team

- name:

  Dispatch User Request to a team

- description:

  Dispatch a user request to a team without assigning an agent

- version:

  1.1.7

- release:

  2018-12-03

- itop-version-min:

  2.1.0

- code:

  combodo-dispatch-userrequest

- diffusion:

  iTop Hub, ITSM Designer

- state:

  stable

- download:

  https://store.itophub.io/en_US/products/combodo-dispatch-userrequest

- alternate-name:

  Dispatch User Request

For iTop versions older than 2.1.0 use a previous version of this component, for iTop 2.1.0 or newer use this version of the component.

**Other versions of this component:** [1.0.1](https://www.itophub.io/wiki/page?id=extensions%3Acombodo_dispatch_userrequest_1_0)

The standard life cycle for User Requests tickets in iTop does not allow to assign a ticket to a Team without assigning it to a specific Person inside this Team. By creating a new state *dispatched*, this extension allows to *dispatch* a User Request ticket to a Team, without assigning it to particular Person. From the *dispatched* state the User Request can then be assigned to a Person.

## Features

Dispatch a User Request to a Team before assigning it to a Person.

The standard User Request life-cycle is the following:

[![Standard User Request Life-cycle](https://www.itophub.io/wiki/media?w=600&tok=29faa4&media=extensions%3Auserrequest-std-lifecycle.png)](https://www.itophub.io/wiki/media-detail?id=extensions%3Acombodo_dispatch_userrequest&media=extensions%3Auserrequest-std-lifecycle.png)

Once the extension has been installed, the User Request life-cycle becomes as follows:

[![User Request Life-cycle with "dispatched" state](https://www.itophub.io/wiki/media?w=600&tok=5f08ce&media=extensions%3Auserrequest-modified-lifecycle.png)](https://www.itophub.io/wiki/media-detail?id=extensions%3Acombodo_dispatch_userrequest&media=extensions%3Auserrequest-modified-lifecycle.png)

The definition of the TTO (Time To Own) metric is also modified to take into account the “dispatched” state (The Time To Own stops when the ticket is actually assigned to a Person, not only dispatched to a Team).

Actually two new states are added to the life-cycle: *dispatched* and *redispatched*, to take into account the first assignment of a ticket. When a ticket which was assigned to a Person is dispatched again to a Team, the agent to which the ticket was assigned is cleared (even if the ticket is dispatched again to the same team).

## Revision History

| Release Date | Version | Comment                                                      |
| ------------ | ------- | ------------------------------------------------------------ |
| 2018-12-03   | 1.1.7   | NL and ES translations                                       |
| 2018-07-02   | 1.1.5   | ES and DE translations                                       |
| 2018-01-26   | 1.1.4   | Update Russian translation (thanks to Vladimir Kunnin)       |
| 2017-10-27   | 1.1.3   | Update German translation (thanks to ITOMIG GmbH)            |
| 2014-11-19   | 1.1.1   | Adapted to iTop > 2.1.0, which gives more flexibility for developing other modules that could add states to the tickets |
| 2014-03-11   | 1.0.1   | Integration of the German translation (thanks to ITOMIG GmbH) |
| 2014-02-28   | 1.0.0   | First version                                                |

## Installation

1. Expand the zip file of the extension and copy the folder `combodo-dispatch-userrequest` into the `extensions` folder of iTop, and make sure that the folder can be read by the web server process.
2. If iTop is already installed, make sure that the configuration file is not read-only
3. Launch the setup program by pointing your browser to http://<itop>/setup/
4. When prompted to select the extensions to install, check “Dispatch of User Requests” and complete the setup.

[![Installation screen](https://www.itophub.io/wiki/media?w=450&tok=73485d&media=extensions%3Adispatch-userrequest-install.png)](https://www.itophub.io/wiki/media-detail?id=extensions%3Acombodo_dispatch_userrequest&media=extensions%3Adispatch-userrequest-install.png)

## Configuration

This extension has no specific configuration setting.

## Usage

The new *dispatched* state is fully integrated with the life-cycle of the ticket. For example, when creating a new User Request, an extra button “Dispatch to a team” appears: [![New button "Dispatch to a team"](https://www.itophub.io/wiki/media?w=600&tok=0a1ab6&media=extensions%3Adispatch-userrequest-new-button.png)](https://www.itophub.io/wiki/media-detail?id=extensions%3Acombodo_dispatch_userrequest&media=extensions%3Adispatch-userrequest-new-button.png)

On an User Request in state *new*, the action “Dispatch to a team..” is available in the drop-down list of actions. [![New action "Dispatch to a team"](https://www.itophub.io/wiki/media?media=extensions%3Adispatch-userrequest-popup-menu.png)](https://www.itophub.io/wiki/media-detail?id=extensions%3Acombodo_dispatch_userrequest&media=extensions%3Adispatch-userrequest-popup-menu.png)

A user must have either the profile “Service Desk Agent” or “Support Agent” (or Administrator) to be allowed to dispatch a ticket.

The list of teams to which the ticket can be dispatched are the same as the ones used when assigning the ticket directly to a Team and a Person. The possible Teams are defined by the Delivery Model of the Organization of the ticket.