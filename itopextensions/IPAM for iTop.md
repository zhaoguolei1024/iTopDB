# IPAM for iTop

- name:

  IPAM for iTop

- description:

  TeemIp application embedded in iTop for full blown IP Address Management

- version:

  2.5.0

- release:

  2019-09-24

- iTop:

  2.6

- code:

  teemip-core-ip-mgmt

- state:

  stable

- keyword:

  [IP Management](https://www.itophub.io/wiki/page?id=keyword&dataflt[0]=keyword_%3DIP Management), [IPAM](https://www.itophub.io/wiki/page?id=keyword&dataflt[0]=keyword_%3DIPAM), [IPv4](https://www.itophub.io/wiki/page?id=keyword&dataflt[0]=keyword_%3DIPv4), [IPv6](https://www.itophub.io/wiki/page?id=keyword&dataflt[0]=keyword_%3DIPv6)

- download:

  https://store.itophub.io/en_US/products/teemip-core-ip-mgmt

IPAM for iTop is the module / extension version of TeemIp that can be integrated on an existing [iTop](http://www.combodo.com/iTop-193) instance. It only provides the core IP management features embbeded in TeemIp standalone. Other features are available for iTop through extensions.

## Compatibility matrix

- For iTop 2.6, use TeemIp 2.5 or TeemIp 2.4
- For iTop 2.5, use TeemIp 2.4 or TeemIp 2.3
- For iTop 2.4, use TeemIp 2.2

If you still rely on older iTop versions, you should seriously consider to migrate. If this is not your intention:

- For iTop 2.3, you may use TeemIp 2.2 or TeemIp 2.1
- For iTop 2.1 and 2.2, you may use TeemIp 2.1 or TeemIp 2.0.3
- For iTop versions lower than 2.0.3, you must use TeemIp 2.0.3

## Installation

#### Automated installation via iTop Hub

This IPAM for iTop extension is available through iTop Hub and can be automatically downloaded and deployed from there. Note that iTop Hub may not be up to date with the latest TeemIp version.

- Go to the [extensions store](https://store.itophub.io/en_US/products/teemip-core-ip-mgmt) on iTop Hub
- Click on the cart icon to make the acquisition of the extension and follow the on-screen instructions to deploy it on your iTop instance

#### Manual installation

- Download [teemip-core-ip-mgmt-2.5.0-478.zip](https://sourceforge.net/projects/teemip/files/teemip - an iTop module/2.5.0/teemip-core-ip-mgmt-2.5.0-478.zip/download) from SourceForge
- Unzip the file “teemip-core-ip-mgmt-2.3.1.zip” into the iTop `extensions` folder
- Make sure that the web server process has enough rights to read the copied files
- Launch iTop setup
- Select the IPAM for iTop extension, when prompted:

[![Select IP Management in the extensions list](https://www.itophub.io/wiki/media?w=500&tok=ad3c5e&media=extensions%3Ateemip-installation-250.png)](https://www.itophub.io/wiki/media?media=extensions%3Ateemip-installation-250.png)

If IP Management does not appear in the list of extensions (or if the whole extensions step is skipped during the setup), make sure that the web server process has enough rights to read the `extensions` directory.