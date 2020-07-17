# Check_mk Data Collector

- name:

  Check_mk Data Collector

- version:

  0.1.0

- release:

  2016-05-20

- description:

  Parses and imports data from check_mk into iTop

- itop-version:

  2.0, 2.1, 2.2

- keyword:

  [inventory](https://www.itophub.io/wiki/page?id=keyword&dataflt[0]=keyword_%3Dinventory), [data synchronization](https://www.itophub.io/wiki/page?id=keyword&dataflt[0]=keyword_%3Ddata synchronization), [check_mk](https://www.itophub.io/wiki/page?id=keyword&dataflt[0]=keyword_%3Dcheck_mk), [nagios](https://www.itophub.io/wiki/page?id=keyword&dataflt[0]=keyword_%3Dnagios), [itomig](https://www.itophub.io/wiki/page?id=keyword&dataflt[0]=keyword_%3Ditomig)

- dependencies:

  itop-config-mgmt

- author:

  ITOMIG GmbH

- download:

  https://odoo.itomig.de/shop/product/check-mk-collector-126

[Download](https://odoo.itomig.de/shop/product/check-mk-collector-126)

This standalone PHP application collects data managed by check_mk's inventory feature. It synchronizes hardware information with an iTop instance using Synchronization Data Sources.

## Features

- Collects Server and PC inventory along with Models, Brands, OS Families and Versions.
- Connects to iTop via the web interface.

## Limitations

Requires direct (read) access to check_mk's inventory files. This means that it must be run on the machine check_mk is installed on (with adequate permissions). Alternatively, the inventory data files used by check_mk must be copied somewhere the application may access them.

Distinguishing between PCs and Servers must be achieved by manually specifying host name patterns. See Configuration below.

## Requirements

- PHP Version 5.3.0
- Read access on check_mk's inventory files
- Access to the iTop REST service

## Installation

- Extract the contents of the archive.
- Edit `conf/params.local.xml` with your iTop credentials.
- Create `collectors/params.distrib.xml` from `collectors/params.template.xml` and edit the configuration options.

README and README_checkmk in the archive's root directory contain further documentation.

## Configuration

### Mandatory parameters

Edit the following parameters in `conf/params.local.xml`:

```
<itop_url>https://localhost/</itop_url>
<itop_login>admin</itop_login>
<itop_password>admin</itop_password>
```

| Parameter     | Meaning                                                      | Sample value           |
| ------------- | ------------------------------------------------------------ | ---------------------- |
| itop_url      | URL to the iTop Application                                  | https://localhost/itop |
| itop_login    | User name for connecting to iTop. Must have admin rights for executing the data synchro. | admin                  |
| itop_password | Password for the iTop account.                               |                        |

These parameters must also be set in `collectors/params.distrib.xml`:

```
<default_org_id>Demo</default_org_id>
<check_mk_dir>/var/lib/check_mk/inventory</check_mk_dir>
<type_mapping type="array">
  <pattern>/.*pc.*/PC</pattern>
  <pattern>/.*srv.*/Server</pattern>
</type_mapping>
```

| Parameter      | Meaning                                                      | Sample value                                                 |
| -------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| default_org_id | The name of the iTop organization under which inventory items should be stored. | Demo                                                         |
| check_mk_dir   | The directory where the collector should check for inventory data files. | /var/lib/check_mk/inventory/                                 |
| type_mapping   | The mapping table which specifies how hosts should be categorized based on their host name in check_mk. Takes patterns in the format `/pattern/replacement`, where `pattern` is a regex matched against the host name and `replacement` must either be `Server` or `PC`. Host names which match no pattern will be ignored. | `<pattern>/.*/Server</pattern>` - catch-all pattern which categorizes all hosts as Servers |

### Optional parameters

The following boolean parameters may be set in `collectors/params.distrib.xml`:

```
<use_network_hostname>false</use_network_hostname>
<skip_gz>true</skip_gz>
<skip_dot>true</skip_dot>
```

| Parameter            | Meaning                                                      | Sample value |
| -------------------- | ------------------------------------------------------------ | ------------ |
| use_network_hostname | Use the host name used on the network by a given inventory machine instead of using the host name stored it is stored under in check_mk. Default is `false`. | false        |
| skip_gz              | When looking for inventory files, skip .gz counterparts if they are found. Default is `true`. | true         |
| skip_dot             | Skip any dotfiles encountered in the inventory file directory. Default is `true`. | true         |

The file `collectors/params.template.xml` contains default values for all configuration items and further documentation on their effects.

### Defaulted fields

It may be useful to give a constant value that should be assigned to a specific field that isn't otherwise filled by the collector. This is done in `collectors/params.distrib.xml`:

```
<default_fields type="hash">
  <field_name>field value</field_name>
  <field_name2>another field value</field_name2>
</default_fields>
```

This is particularly useful for fields such as `status` and `business_criticity` if they are in use. Only fields which both Servers and PCs have should be specified this way.

## Data mapping

The data in check_mk is gathered from a variety of sources and thus may not always fit the existing iTop data. A mapping table is used to define how data should be converted to fit in with your needs when the above items are being added to iTop.

In this collector, this applies to Brand, OS Family and OS Version objects.

Mapping tables are edited in `collectors/params.distrib.xml`. The file `collectors/params.template.xml`, supplied in the archive, contains examples and further documentation.

Example:

```
<osfamily_mapping type="array">
  <pattern>/.*linux.*/Linux</pattern>
  <pattern>/.*windows.*/Windows</pattern>
  <pattern>/.*mac os.*/Mac OS</pattern>
  <pattern>/.*solaris.*/Solaris</pattern>
  <pattern>/.*bsd.*/BSD</pattern>
  <pattern>/.*/$1$s</pattern>
</osfamily_mapping>
```

This will map Linux, Windows, Mac OS, Solaris and BSD OS family variations. `<pattern>/.*/$1$s</pattern>` will allow the collector to add any values which don't fit any other patterns to iTop without manipulating them.

Omit `<pattern>/.*/$1$s</pattern>` if you want OS Families (or OS Versions or Brands) which are not otherwise defined in the mapping table to be ignored. This is the default behaviour.

## Usage

The first time the collector is run, the following command is recommended:

```
php exec.php --configure_only
```

This will create the Synchronization Data Sources if they don't already exist.

To collect the data without synchronizing with iTop, run

```
php exec.php --collect_only
```

This will store the collected data in CSV files in the `data/` subdirectory of the collector - this is useful for checking the data before it is passed over to iTop. Mapped values can be checked and mapping tables updated - however, note that collection should be run again after such changes.

Finally, to perform iTop synchronization with the data collected:

```
php exec.php --synchro_only
```

Data collection and synchronization (and data source update/creation if necessary) can be performed in a single step if desired:

```
php exec.php
```

While this is simpler, it affords less control over the synchronization process.

More information on running the collector may be found on the [itop-data-collector-base](https://www.itophub.io/wiki/page?id=extensions%3Aitop-data-collector-base) page.

## Data Collection Reference

### Servers and PCs

Servers and PCs have the same data collected about them.

| Field in iTop | check_mk inventory entry                                     |
| ------------- | ------------------------------------------------------------ |
| name*         | The check_mk host name, which is the name of the check_mk inventory data file, or networking host name (see Configuration above) |
| org_id*       | Taken from default_org_id in configuration                   |
| cpu           | hardware → cpu → model                                       |
| ram           | hardware → memory → total_ram_usable (in MiB)                |
| osfamily_id   | Mapped using data in either software→os→type or software→os→name using osfamily_mapping pattern list |
| osversion_id  | Mapped from software→os→name using osversion_mapping pattern list |
| serial        | hardware → system → serial                                   |
| brand_id      | Mapped from hardware→system→vendor using brand_mapping pattern list |
| model_id      | Mapped from hardware→system→family                           |

\* denotes mandatory fields - the rest can and will be ignored if the relevant data is not present in check_mk without preventing the object from being synchronized.