# SLA considering business hours

- name:

  SLA considering business hours

- description:

  Compute SLAs taking into account service coverage window and holidays

- version:

  2.1.12

- release:

  2018-12-19

- itop-version-min:

  2.0.2

- dependencies:

  itop-service-mgmt or itop-service-mgmt-provider, itop-sla-computation

- code:

  combodo-sla-considering-business-hours

- download:

  https://store.itophub.io/en_US/products/combodo-sla-considering-business-hours

- alternate-name:

  SLA with Coverage Windows

**Compatibility issue**: for iTop version lower than 2.4.0, there is a [special installation/upgrade process](https://www.itophub.io/wiki/page?id=extensions%3Ainstallation#itop_before_240).

For iTop versions older than 2.0.2 use a previous version of this component

**Other versions of this component:** [1.0](https://www.itophub.io/wiki/page?id=extensions%3Acoverage_wondow_sla_computation), [2.0.2](https://www.itophub.io/wiki/page?id=extensions%3Asla-computation_2_0)

This extension adds the capability to define Coverage Windows and Holidays in iTop and use them to compute *Service Level Agreements* (SLA) deadlines depending on the service and the coverage windows used in the customer contracts.

Compared to the 2.0.x version(s) this new version adds the support of an arbitrary number of open hours intervals per day.

## Features

By default, SLA computation assumes that a given duration does not depend on the time it starts (i.e. computations are based on a 24×7 service).

If you would like to compute SLA deadlines (TTO and TTR) depending on the customer/service and the times at which your support teams are working, then you will have to implement Coverage windows.

This extension allows you to define:

- Coverage windows (i.e. open hours within each day of the week), possibly as several intervals with the day (i.e. integrate a lunch break)
- Holidays (complete days which are closed for business, e.g. January 1st, May 1st…)
- How the Coverage Windows and Holidays are related to each Ticket.

Once the Holidays and Coverage Windows are created in the system, the TTO and TTR deadlines are computed according to the corresponding coverage windows and exclude the holidays.

The conversion from previous format(s) of Coverage Windows is automatic, during the installation of the module.

## Revision History

| Release Date | Version | Comments                                                     |
| ------------ | ------- | ------------------------------------------------------------ |
| 2018-12-19   | 2.1.12  | - Update translations - Improve jQuery compatibility (jQuery 3 since iTop 2.6) |
| 2018-06-26   | 2.1.10  | New translations (ES, BR)                                    |
| 2017-03-28   | 2.1.9   | Bug fix: Corruption of coverage windows when edited from a browser having a timezone different from the timezone of iTop |
| 2016-03-15   | 2.1.7   | Prevent overflow of an interval to the next day when dragging/dropping this interval in the calendar. |
| 2015-09-30   | 2.1.6   | Removed the “plus” button from the link Contract/Service, to workaround a bug in the coverage windows creation form (when shown as a dialog). Will be fixed later in the core of iTop. This regression has been introduced in the version 2.1.0 of the component and is related to the management of multiple time intervals. |
| 2015-09-24   | 2.1.5   | No change but a module version that is now consistent with our records (combodo-sla-computation: 2.1.5). |
| 2015-06-30   | 2.1.4   | Protects against “empty” days (i.e. days for which no interval exists) which generated a warning. |
| 2014-12-18   | 2.1.3   | Do not overwrite the value of 'coverage_oql' in the configuration file if the value was modified. |
| 2014-12-09   | 2.1.2   | Bug fix in the computation due to internal mismatches with timezones! |
| 2014-12-01   | 2.1.1   | Bug fix in the computation (1 min skipped from the end of intervals) and some cosmetics enhancements. |
| 2014-11-26   | 2.1.0   | Support of multiple open hours intervals per day.            |
| 2014-03-11   | 2.0.1   | Integration of the German translation (thanks to ITOMIG GmbH) |
| 2014-03-04   | 2.0.0   | Offical release of the 2.0.0 version which requires iTop 2.0.2 or newer, but supports nice formatting (i.e. 19:45 instead of 19,75) for the times. If you need a version compatible with iTop 2.0.1 or older, use [Coverage Window Sla Computation (legacy)](https://www.itophub.io/wiki/page?id=extensions%3Acoverage_wondow_sla_computation) |

## Limitations

Holidays are not taken into account if no coverage window has been defined (or if none applies to the ticket).

## Requirements

iTop 2.0.2 or newer.

## Installation & upgrade

- Download the package: and expand the content of the zip folder into the “**extensions**” directory of iTop.

**Compatibility issue**: for iTop version lower than 2.4.0, there is a [special installation/upgrade process](https://www.itophub.io/wiki/page?id=extensions%3Ainstallation#itop_before_240).

- If you have already installed iTop, make sure that the configuration file `config-itop.php` in `conf/production` is NOT read-only.
- Point your web browser to `http(s)://<your_itop_root>/setup` and follow the wizard instructions. Make sure that you select the option to “Upgrade an existing iTop instance”:[![img](https://www.itophub.io/wiki/media?w=300&tok=c529d3&media=extensions%3Aemail-upgrade-screenshot1.png)](https://www.itophub.io/wiki/media?media=extensions%3Aemail-upgrade-screenshot1.png)[![img](https://www.itophub.io/wiki/media?w=300&tok=2a82a7&media=extensions%3Aemail-upgrade-screenshot2.png)](https://www.itophub.io/wiki/media?media=extensions%3Aemail-upgrade-screenshot2.png)
- Finally check the module “Plug-in SLA computation with coverage windows for UserRequest and Incidents” in the list of extensions at the end of the interactive wizard. Then complete the installation.

[![img](https://www.itophub.io/wiki/media?w=300&tok=b1d117&media=extensions%3Acombodo-sla-computation-install-module.png)](https://www.itophub.io/wiki/media?media=extensions%3Acombodo-sla-computation-install-module.png)

## Configuration

Once the new module has been installed, the default configuration states that:

- The Coverage Window applicable to a Ticket is defined, for each Service, on the Customer Contract.
- There is just one global list of Holidays. Any Holiday defined is applicable to any Ticket.

```
        'combodo-sla-computation' => array (
                'coverage_oql' => 'SELECT CoverageWindow AS cw JOIN lnkCustomerContractToService AS l1 ON l1.coveragewindow_id = cw.id JOIN CustomerContract AS cc ON l1.customercontract_id = cc.id WHERE cc.org_id= :this->org_id AND l1.service_id = :this->service_id',
                'holidays_oql' => 'SELECT Holiday',
        ),
```

You can adjust the configuration parameters if you want to use different rules.

| Parameter name | Description                                                  | Default Value                                                |
| -------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| coverage_oql   | The OQL to retrieve the Coverage Window object to apply to a given ticket. If the query returns several Coverage Window objects, **only the first one** will be used. | `SELECT CoverageWindow AS cw  JOIN lnkCustomerContractToService AS l1   ON l1.coveragewindow_id = cw.id  JOIN CustomerContract AS cc   ON l1.customercontract_id = cc.id  WHERE cc.org_id= :this->org_id  AND l1.service_id = :this->service_id` |
| holidays_oql   | The OQL to retrieve the Holiday objects to apply to a given ticket. **All** the Holidays returned by the query will be taken into account for the computation. | SELECT Holiday                                               |

The two OQL queries listed above are relative to a Ticket (the current ticket being processed). This means that all the placeholders `:this->xxx` refer to the corresponding fields of the Ticket.

You can also change the display format of the TTO and TTR deadlines by modifying the configuration parameter **deadline_format** in `config-itop.php` with the following value:

```
        'deadline_format' => '$date$ ($difference$)',
```

This will display the deadline date and the delay from now to the dealine.

## Usage

### Managing Coverage Windows

The menu “Coverage windows” in the module “Service management” displays all coverage windows defined in iTop. If none has been defined click on “Create a new coverage window”, otherwise click on “Create” to create a new one.

The open hours for a given “Coverage Window” object are represented as a set of intervals, for each day of the week. The area outside of the blue intervals is considered as “Off hours”.

[![Coverage Window Edition ](https://www.itophub.io/wiki/media?w=500&tok=23dbcb&media=extensions%3Acoverage_window_intervals.png)](https://www.itophub.io/wiki/media?media=extensions%3Acoverage_window_intervals.png)

The intervals are edited directly in the calendar at the bottom of the page:

- Click and drag over an empty area to create a new interval
- Drag the handle at the bottom of an interval to adjust its duration
- Drag the interval around to change its starting time
- Click inside an interval to open a dialog box in order to edit the interval's properties

When clicking on an interval, the following dialog is displayed:

[![Open Hours Interval Edition ](https://www.itophub.io/wiki/media?w=300&tok=e278d2&media=extensions%3Acoverage_window_interval_edition.png)](https://www.itophub.io/wiki/media?media=extensions%3Acoverage_window_interval_edition.png)

Click on “Remove Interval” to completely remove an interval from the coverage window.

All the modifications to the intervals are applied only when cliking on the “Apply” button to submit the modifications to the Coverage Window object as a whole.

### Managing Holidays

The menu “Holidays” in the module “Service management” displays all holidays defined in iTop. If none has been defined click on “Create a new holiday”, otherwise click on “Create” to create a new one.

[![img](https://www.itophub.io/wiki/media?w=200&tok=1db98c&media=extensions%3Acombodo-sla-computation-screnshot3.png)](https://www.itophub.io/wiki/media-detail?id=extensions%3Asla-computation&media=extensions%3Acombodo-sla-computation-screnshot3.png)

The Holiday Calendar allows you to group holidays (for example based on the country of your customers). This is a convenient way to simplify the queries required by a complex (multi-customer / multi-country) environment.

The OQL queries configured by default when installing the module do not use Holiday Calendars but Holidays.

### Select coverage windows for a customer

To change the coverage window of a customer contract, simply modify the contract and in the tab “Services” select the appropriate coverage window required for each service:

[![img](https://www.itophub.io/wiki/media?w=800&tok=464f8d&media=extensions%3Acombodo-sla-computation-screnshot4_noplus.png)](https://www.itophub.io/wiki/media-detail?id=extensions%3Asla-computation&media=extensions%3Acombodo-sla-computation-screnshot4_noplus.png)

By default, if no coverage window is selected, the computation of deadlines will be done using a 24h*7 coverage window.