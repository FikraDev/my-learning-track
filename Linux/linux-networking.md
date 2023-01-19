# **Networking in Linux**

## Networking Basics

- IP address
- Subnet Mask
- Gateway
- Static vs DHCP
- Interface
- Interface MAC Address - 12 dash seperated characters.  The first six (6) characters uniquely identify the manufacturer of the device.  the other six identify that Network Interface Controller (NIC).

## Must Know Configuration Files

- Interface configuration files are:
  - **/etc/nsswitch.conf** -  used to configure which services are to be used to determine information such as hostnames, password files, and group files.
  - **/etc/hosts** - this file contains the Internet Protocol (IP) host names and addresses for the local host and other hosts in the Internet network.  It is used to map hostnames to IP addresses.  It acts like a local DNS server.  It is located in the /etc directory which means that in order to edit it you have to use elevated privleges(sudo/root).
    - the first entries in the file are normally dedicated to the host machine.
  - **/etc/hostname** - this is the local hostname configuration file.  It is used to configure the nameof the local system.
  - **/etc/sysconfig/network** - specifies routing and host information for all network interfaces. **(Rhel derived variants)**
  - **/etc/network/interfaces** - allows for the definition of static and dynamic IP addresses for the interfaces, setup routing information and default gateways, masquerading network bonding and more.
    - the default interfaces file will only have:
    > `auto lo` - auto starts the interface at boot
    > `iface lo inet loopback` - calls the network interface

  - **/etc/resolv.conf**

### How to Setup an Interface with DHCP by Editing the /etc/network/intefaces file

> `auto <Interface> <br>
> allow-hotplug <Interface> <br>
> iface <Interface> inet dhcp`

Where allow-hotplug will start the interface upon event detection.
