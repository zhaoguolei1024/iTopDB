# Hyperlinks configurator

- name:

  Hyperlinks configurator

- description:

  Create hyperlink actions on object via configuration parameters

- version:

  1.0.2

- release:

  2019-03-15

- itop-version-min:

  2.3.0

- code:

  combodo-custom-hyperlinks

- download:

  https://store.itophub.io/en_US/products/combodo-custom-hyperlinks

Create hyperlink buttons to jump from one object in iTop into another application, via configurable URLs, without writing a single line of code.

## Features

- Hyperlink, label, tooltip and icon are configurable
- The `scope` option makes it possible to display the hyperlink only on objects matching a specific rule
- The target of the link is configurable as well (by default `_blank` to open the link in another tab/window)
- The `contexts` option specifies if the link is available in the backoffice (console) and/or in the portal(s) (and in which portal if there are several of them).
- The action/button can be limited to users having at least one of the `allowed_profiles`.

## Revision History

| Version | Release Date | Comments                                                     |
| ------- | ------------ | ------------------------------------------------------------ |
| 1.0.2   | 2019-03-19   | Add it on Portal objects with scope Add “allowed_profiles” parameter |
| 1.0.1   | 2019-03-15   | Addition of the “tooltip” and “contexts” parameters          |
| 1.0.0   | 2019-02-07   | First version                                                |

## Limitations

- Button labels cannot be localized (they are not dictionary entries)

## Requirements

iTop 2.3.0 or newer

## Installation

Deploy it via iTop Hub or ITSM Designer

## Configuration

For each “link” to be displayed, the following configuration parameters are available:

| Parameter          | Mandatory?           | Meaning                                                      | Example                                                      |
| ------------------ | -------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| `label`            | mandatory if no icon | The label of the button/link                                 | Wikipedia                                                    |
| `url`              | mandatory            | The hyperlink to jump to                                     | `https://www.wikipedia.org/wiki/$this->first_name$_$this->name$` |
| `target`           | optional             | where to display the url result `_blank` for a new window *default*, `_top` for the current window | `_blank`                                                     |
| `scope`            | optional             | An OQL query to filter on which object to display this link  | `SELECT Contact WHERE org_id = 2`                            |
| `icon`             | optional             | A Font Awesome 4.7 icon code                                 | `wikipedia`                                                  |
| `tooltip`          | optional             | The label of a tooltip to display on the item. *default*: no tooltip | Jump to Wikipedia                                            |
| `contexts`         | optional             | If specified, a comma separated list of portals in which to enabled this link. Use `backoffice` for the iTop console. If not specified, it's available in all contexts | `backoffice,itop-portal`                                     |
| `allowed_profiles` | optional             | If specified, a comma separated list of iTop Profiles for which to enable this link. If not specified, all profiles are allowed. | `Support Agent,Configuration Manager`                        |

This extension does not bring very useful links without a proper configuration specific to your environment and needs

```
'combodo-custom-hyperlinks' => array (
   'hyperlinks' => array (
      'Person' => array (
         'linkedin_me' => array (
            'label' => 'Linkedin Me!',
            'url' => 'https://www.linkedin.com/search/results/all/?keywords=$this->friendlyname$',
            'scope' => 'SELECT Contact WHERE org_id_friendlyname=\'demo\'',
            'icon' => 'linkedin',
         ),
      ),
      'Location' => array (
         'maps_me' => array (
            'label' => 'GoogleMaps Me!',
            'url' => 'https://www.google.com/maps/search/$this->address$+$this->postal_code$+$this->city$+$this->country$',
            'scope' => 'SELECT Location WHERE org_id_friendlyname=\'demo\'',
            'icon' => 'globe',
         ),
      ),
   ),
),
```

You can also display the hyperlink as a button (next to the “Other actions…” menu) by specifying its UID in the configuration parameter 'shortcut_actions'

The icons are displayed using the Font Awesome font (already included in iTop). Therefore the icon codes to use are the [Font Awesome 4.7 codes](https://fontawesome.com/v4.7.0/icons/)

## Usage

Just click on the button(s) !

[![img](https://www.itophub.io/wiki/media?w=600&tok=c20509&media=extensions%3Ahyperlinks-configurator-linkedin.png)](https://www.itophub.io/wiki/media-detail?id=extensions%3Acombodo-custom-hyperlinks&media=extensions%3Ahyperlinks-configurator-linkedin.png)*[![img](https://www.itophub.io/wiki/media?w=600&tok=b66b09&media=extensions%3Ahyperlinks-configurator-googlemaps.png)](https://www.itophub.io/wiki/media-detail?id=extensions%3Acombodo-custom-hyperlinks&media=extensions%3Ahyperlinks-configurator-googlemaps.png)*