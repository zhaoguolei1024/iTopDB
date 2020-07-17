# Calendar view

- name:

  Calendar view

- description:

  Displays elements inside a monthly, weekly or daily calendar

- version:

  2.0.2

- release:

  2019-07-02

- itop-version-min:

  2.4.0

- code:

  combodo-calendar-view

- state:

  stable

- download:

  https://store.itophub.io/en_US/products/combodo-calendar-view

- diffusion:

  iTop Hub

You want to:

- See your **planned Changes on a calendar** view?
- Get a quick overview of **contracts ending next month**?
- Visualize Physical **Devices reaching End of warranty** on a timeline view?

Then this extension is for you.

## Features

This extension brings a **new Calendar Dashlet which can be added to any Dashboard**

From a user perspective

- Objects are displayed on a calendar view, as meetings in a google calendar,
- Objects can have a **different color** depending on a field value (*status for eg.*),
- User can switch between **Day, Week, Month or List** display modes,
- User can navigate to the **next** or the **previous** day/week/month,
- User can choose to **hide** some groups of objects, within the displayed ones,

## Revision History

| Date       | Version | Description                                                  |
| ---------- | ------- | ------------------------------------------------------------ |
| 2019-07-02 | 2.0.2   | - Fix assets being kept in cache                             |
| 2019-06-20 | 2.0.1   | - Rename dictionnaries files - Fix script loader when more than one calendar is displayed - Security hardening |
| 2018-08-13 | 2.0.0   | New version generic version of the extension, fully customizable without any code. |

## Limitations

It's not possible to display FunctionalCIs at the date of a Change they are linked to. The date field must be an attribute of the displayed object.

## Requirements

- iTop 2.4 or later

## Installation

Use the [Standard installation process](https://www.itophub.io/wiki/page?id=extensions%3Ainstallation) for this extension.

## Configuration

Some configuration parameters are available for this extension:

| Parameter                  | Description                                                  | Default |
| -------------------------- | ------------------------------------------------------------ | ------- |
| **default_scope_count**    | Default number of scopes when creating a new dashlet         | *3*     |
| **max_scope_count**        | Maximum number of scopes a dashlet can have. This parameter is for all calendar view dashlets. | *10*    |
| **default_event_duration** | Default duration in minutes for events that have only a start or end date. | *30*    |
| **first_day**              | First day of week. This parameter is for all calendar view dashlets, no matter the user language. Value can be 0 (sunday), 1 (monday), … | *1*     |
| **business_hours**         | Highlighted period of the week in dashlets (events can be created outside this period). A PHP array containing the *days_of_week* (same pattern as the *first_day* parameter, default is *array(1,2,3,4,5)*), *start* hour (default is *09:00*), *end* hour | *18:00* |

```
  'combodo-calendar-view' => array (
                'default_scope_count' => 4,
                'max_scope_count' => 10,
                'default_event_duration' => 15,
                'first_day' => 1,
                'business_hours' => array (
                  1 => '08:00, 19:00',
                  2 => '08:00, 19:00',
                  3 => '08:00, 19:00',
                  4 => '08:00, 19:00',
                  5 => '08:00, 19:00',
                ),
        ),
```

## Usage

### Designing a Calendar Dashlet

The Dashlet designer specifies

- the objects displayed in the Dashlet as scopes
- sub-groups of object based on a field (*groups per status for example*)
- the colors to use per group of object,
- the default display mode,….

Calendar Dashlet can display objects from **any class** as long as it has at least **one date or date-time** field

| Property        | Purpose                                                      |
| --------------- | ------------------------------------------------------------ |
| Title           | Title is displayed on the top banner of the calendar, it can be a dictionary entry eg. UI:RequestMgmtMenuOverview:Title |
| Default display | This is the default display mode, which is used when the dashboard is displayed, the user can still change the display mode, but it is not recorded. Next refresh of the page will restore the default display |
| Scope count     | Change this number if you want to define more than 3 groups of objects to display in the same dashlet. It will expend the form with more scopes. When saving empty scopes are ignored |

|             | scopes #                                                     |
| ----------- | ------------------------------------------------------------ |
| Name        | Label of the scopes as displayed in the selection bar        |
| OQL         | An OQL query which must return a **single** class of objects to display |
| Start date  | A mandatory date or date-time field of the above class, which is used as the start time for displaying the object in the calendar. |
| End date    | An optional date or date-time field of the above class, which is used as the end time for displaying the object in the calendar. |
| Description | An optional field which value will be displayed in a tooltip while moving your mouse above an object |
| Group by    | An optional field to divide your scopes in groups.           |
| Items color | A fixed selection of predefined colors, plus an extra “Rainbow (multicolors)” |
| Colors mode | `Plain` which is the default, means every groups will use the same colors, `Shades` means a different shade of the color will be used for each group |

- If `date` attribute (*without time*) is used either the Start date or the End date, the objects are displayed as full-day event in Daily and Weekly display mode.
- `Group by` field values will displayed under the scope name, hidden by default.

![img](https://www.itophub.io/wiki/media?w=300&tok=0bddd4&media=extensions%3Acalendar-filter-shades2.png)

- If “Rainbow (multicolors)” is selected then each group will get a different plain color, instead of a different shade of a unique color.

![img](https://www.itophub.io/wiki/media?w=300&tok=a708b9&media=extensions%3Acalendar-filter-rainbow2.png)

- If no `Group by` field is selected, then `Colors mode` is useless and “Rainbow (multicolors)” is equivalent to “Orange”.

#### Example

Here is an example with 2 scopes, both with groups.

- Physical Devices uses a purple “shades” grouping by “brand”
- Changes uses a “Rainbow” grouping by “status”

![img](https://www.itophub.io/wiki/media?w=500&tok=e046f5&media=extensions%3Acalendar-configure2.png)

### Using a Dashlet Calendar

Here the display of the same example as below.

- Change uses a **date-time** Start date and **Start date** End date, so object are displayed with their duration (Object with **no** End date will be displayed with a duration defined in the Extension configuration parameter default_event_duration),
- Physical Device uses a **date** End warranty date, which means object are displayed as “all day” events in Daily and Weekly display modes

The default display mode of our example is a Week

![img](https://www.itophub.io/wiki/media?w=600&tok=718b81&media=extensions%3Acalendar-display2.png)

User can decide to hide some of the groups by opening the criteria and un-selecting some groups

![img](https://www.itophub.io/wiki/media?w=800&tok=fc519e&media=extensions%3Acalendar-select-group2.png)

User can switch to a different display mode, such as List for a month:

![img](https://www.itophub.io/wiki/media?w=600&tok=a3d0b1&media=extensions%3Acalendar-list2.png)

or Month displayed as a table with one row per week and one cell per day:

- **Full day** object have a colored background behind their name
- Object with a **starting hour**, have a colored bullet in front of its name

![img](https://www.itophub.io/wiki/media?w=600&tok=853074&media=extensions%3Acalendar-month2.png)

When there are too many objects in a cell, a number of not-yet-displayed objects is provided and you can click on it to display the complete list of objects for that day.

![img](https://www.itophub.io/wiki/media?w=400&tok=2047b4&media=extensions%3Acalendar-month-more2.png)

On any object displayed, moving the mouse over it display a tooltip with

1. the friendlyname,
2. the description,
3. the Start date,
4. End date,
5. The scope name and the group value in parentheses

![img](https://www.itophub.io/wiki/media?w=600&tok=7cf0f3&media=extensions%3Acalendar-day4.png)