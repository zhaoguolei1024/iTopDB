# Location Hierarchy

- name:

  Location Hierarchy

- description:

  Organize your locations in hierarchy and retrieve CIs located on a location tree

- version:

  1.0.1

- release:

  2019-05-16

- itop-version-min:

  2.4.0

- code:

  combodo-location-hierarchy

- state:

  Stable

With iTop products older than 2.7.0, when you add this extension through the **ITSM Designer**, existing Locations will loose their friendlyname. **Run a Setup** to fix this.

Once you have installed this extension, your locations will be enriched with those fields:

- a **type**, which can be one of those: **Site, Building, Floor, Room** and **Tile** in decreasing order (*default: Site*)
- an optional **parent location**, which is can be chosen among Locations with an higher type.
- a flag to either inherit Address, Zip, Site and Country from its location parent or define its own (*default: inherit*)

## Features

#### Location parent

- The parent location is optional
- It can belong to any organization, it's not limited to the same organization as the edited location.
- The parent location is expected to be of a type above or equal to the current location type. Eg. a `Room` can have a `Building` as parent, but also a `Site` or even another `Room`

#### Location name

- The full name of a Location is calculated based on the site hierarchy, with the following logic: name of parents, separated with a defined parameter and ordered from top to current location name.
- This full name is computed when
  - location parent is set or modified
  - name is modified
- When full name is modified, all sub-locations full name are recomputed.
- The separator of names is by default a dash between 2 white-spaces ' - ', but it can be changed in the module configuration parameter.

#### Location address

A flag `Address ?` allow to say for a child location if the `Address`, `Zip`, `City` and `Country` should be automatically copied from the parent location, thus avoiding duplicate entries and incoherence if parent address is modified later.

- If you defined a parent and leave the flag to `copied from parent if defined`, then any entry you do in `Address`, `Zip`, `City` and `Country` will be overwritten by values from the parent.
- If no parent is defined, that flag has no effect.

#### Sub-location

A new tab display the direct sub-locations of the current location

#### Search of Physical Devices or Contacts

When searching for Physical Devices (or Contacts) located on a given Location, iTop will now return all Physical Devices (or Contacts) located on that Location **or on any child location below in the hierarchy**.

#### Location and silos

As you can define sub-sites under a site belonging to different organizations, you can segment your CIs, putting them on a Location within their silo and still be able to see all CIs from all organizations located on the parent site or any sub-locations down the hierarchy.

## Revision History

| Date       | Version | Description                                               |
| ---------- | ------- | --------------------------------------------------------- |
| 2019-05-16 | 1.0.1   | Fix PHP warning “missing 3rd parameter GetAttributeFlags” |
| 2019-02-27 | 1.0.0   | First official version                                    |
| 2018-12-24 | 0.1.0   | First version                                             |

## Limitations

- It proposes exactly five types of Location, to have less or more you need to customize [Q&A](https://www.itophub.io/wiki/page?id=extensions%3Acombodo-location-hierarchy#questions_answers).
- Name ordering is “parent before child” and can be changed only by customization.
- As the Location `presentation` is fully redefined by this extension, it can conflict with other extensions which would modify as well the Location class.

If a location type is changed, there is no control that its children locations types are still aligned with the types order.
*Example if you change a 'Site' location having 'Buildings' sub_locations under it, into a 'Room' type of Location, then the 'Buildings' would still remain under the 'Room' also it's not logical. If you modify one of those 'Building' and remove the 'Room' parent, once submitted, it won't be possible to put it back.*

## Requirements

Have a `Location` class on your iTop, not customized by other extensions.

## Installation

Use the [Standard installation process](https://www.itophub.io/wiki/page?id=extensions%3Ainstallation) for this extension.

If you install this extension through a Move To Production **from the ITSM Designer** on an iTop with already created Locations, then **you must run a Setup** manually after, otherwise your Locations would appear with no friendlyname

## Configuration

Once the new module has been installed, edit the configuration file config-itop.php and look for the following new section:

```
  'combodo-location-hierarchy' => array (
                'separator' => ' - ',
        ),
```

## Usage

This is how a list of locations will look like![img](https://www.itophub.io/wiki/media?media=extensions%3Alocation-hierarchy-list.png)

The details of a Location with its sub-locations:![img](https://www.itophub.io/wiki/media?media=extensions%3Alocation-hierarchy-view.png)

Editing the parent location, limited to those of a higher Type level:![img](https://www.itophub.io/wiki/media?media=extensions%3Alocation-hierarchy-edit.png)

Searching for PhysicalDevices located on a Location or any location below that one:![img](https://www.itophub.io/wiki/media?media=extensions%3Alocation-hierarchy-searchcis.png)

## Questions & Answers

**Question: I need different values for Location types, can I change them?**
Answer: Yes, you can do this through an extension which would modify the dictionary entries

```
<dictionaries>
  <dictionary id="EN US" _delta="define_if_not_exist">
    <entries>
      <entry id="Class:Location/Attribute:type/Value:1" _delta="force"><![CDATA[Campus]]></entry>
      <entry id="Class:Location/Attribute:type/Value:2" _delta="force"><![CDATA[Site]]></entry>
      <entry id="Class:Location/Attribute:type/Value:3" _delta="force"><![CDATA[Tower]]></entry>
      <entry id="Class:Location/Attribute:type/Value:4" _delta="force"><![CDATA[Floor]]></entry>
      <entry id="Class:Location/Attribute:type/Value:5" _delta="force"><![CDATA[Room]]></entry>        
    <...>
```

**Question: I would like less (or more) than 5 level of Locations, how can I do?**
Answer: Yes, you can do this through an extension which would modify the possible values for `type` field.

```
<itop_design>
  <classes>
    <class id="Location">
      <fields>
        <field id="type" _delta="must_exist">
          <values _delta="redefine">
            <value id="1">1</value>
            <value id="2">2</value>
            <value id="3">3</value>
            <value id="4">4</value>
          </values>
        </field>
      <...>
```

If you add level don't forget to add also dictionary entries for the newly created level. Use numeric values in decreasing order (parent location having a lower value than its sub-locations) or you will break the proposed parent logic.

**Question: Can I prevent location of a same type to be proposed as parent?**
Answer: Yes, you can do this through an extension which would modify the parent filter

```
<itop_design>
  <classes>
    <class id="Location">
      <fields>
        <field id="parent_id" _delta="must_exist">
          <filter _delta="redefine">
            <![CDATA[SELECT Location WHERE (type < :this->type)]]>
          </filter>
        </field>
      <...>
```

**Question: I have found a floor location which is the parent of a site location, how is it possible?**
Answer: When you modify the `type` of a location, it does not check nor modify the types of the locations above and under the one you modify, so it is possible to break the hierarchy logic this way. You can build an audit rule to check such unexpected situation:![img](https://www.itophub.io/wiki/media?w=400&tok=9b202b&media=extensions%3Alocation-hierarchy-audit-category.png)![img](https://www.itophub.io/wiki/media?w=500&tok=83b316&media=extensions%3Alocation-hierarchy-audit-rule.png)

```
SELECT Location AS p JOIN Location AS c ON c.parent_id BELOW p.id WHERE p.type > c.type
```

**Question: I want that the fullname of Location uses the reverse order of the hierarchy?**
Answer: Check the Location method `UpdateFromParent` and change this line:

```
$this->Set('fullname', $sParentName.$sSeparator.$sName);
```

to replace by this one:

```
$this->Set('fullname', $sName.$sSeparator.$sParentName);
```