# Admin tools delegation

- name:

  Admin Tools Delegation

- description:

  This extension create new profiles to delegate admin tools menus, so you can give any of those responsibility

- version:

  0.1.0

- release:

  2017-07-05

- download:

  https://store.itophub.io/en_US/products/itop-admin-delegation-profiles

- code:

  itop-admin-delegation-profiles

This extensions add new user profiles to your iTop.

Those added profiles **are not self-sufficient**. They must be combined with another profile such as `Configuration Manager`, `Service Manager`,…

## Features

The new profiles brought by this extension:

| Profile                | Associated priviledges                                       |
| ---------------------- | ------------------------------------------------------------ |
| *User Manager*         | Has the rights to create/modify/delete users…                |
| *Notification Manager* | Has the rights to create and modify triggers and actions     |
| *Audit Manager*        | Has the rights to create and modify Audit (categories and rules) |
| *Query Manager*        | Has the rights to create and modify the Query Phrasebook     |
| *SynchroData Manager*  | Has the rights to create and modify Synchro data sources     |
| *Admin Tools Manager*  | Has the rights to do all the above listed actions            |

## Revision History

| Date       | Version | Description    |
| ---------- | ------- | -------------- |
| 2017-07-05 | 0.1.0   | First version. |

## Limitations

None

## Requirements

Requires iTop 2.5.0 or above

## Installation

Use the [Standard installation process](https://www.itophub.io/wiki/page?id=extensions%3Ainstallation) for this extension.

## Configuration

No configuration parameters for this extension

## Usage

Once installed, the Administrator will be able to give those profiles to users, as any other standard profiles.

Those added profiles **are not self-sufficient**. They must be combined with another profile such as `Configuration Manager`, `Service Manager`,…

Each of this profile will give access to the *Admin Tools* header menu, with specific sub-menus:

| Profile              | Menus included               |
| -------------------- | ---------------------------- |
| User Manager         | User Accounts, Profiles      |
| Audit Manager        | Audit, Run Query             |
| Notification Manager | Notification, Run Query      |
| Query Manager        | Query Phrasebook, Run Query  |
| SynchroData Manager  | Synchronization Data Sources |
| AdminTools Manager   | *all menus above*            |

Example of a the `Admin Tools` menu for a user having profile `Notification Manager` & `Audit Manager`![img](https://www.itophub.io/wiki/media?media=extensions%3Amenuadmintools-notifmanager.png)