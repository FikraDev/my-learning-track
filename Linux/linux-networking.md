# **Networking in Linux**

## Networking Basics

- IP address
- Subnet Mask
- Gateway
- Static vs DHCP
- Interface
- Interface MAC Address - 12 dash seperated characters.  The first six (6) characters uniquely identify the manufacturer of the device.  the other six identify that Network Interface Controller (NIC).

## Must Know Configuration Files

- The must know interface configuration files are:
  - **/etc/nsswitch.conf** -  used to configure which services are to be used to determine information such as hostnames, password files, and group files.
  - **/etc/hosts** - this file contains the Internet Protocol (IP) host names and addresses for the local host and other hosts in the Internet network.  It is used to map hostnames to IP addresses.  It acts like a local DNS server.  It is located in the /etc directory which means that in order to edit it you have to use elevated privleges(sudo/root).
    - the first entries in the file are normally dedicated to the host machine.
  - **/etc/hostname** - this is the local hostname configuration file.  It is used to configure the name of the local system.
  - **/etc/sysconfig/network** - specifies routing and host information for all network interfaces. **(Rhel derived variants)**
  - **/etc/network/interfaces** - allows for the definition of static and dynamic IP addresses for the interfaces, setup routing information and default gateways, masquerading network bonding and more.
    - the default interfaces file will only have:

    > auto lo - auto starts the interface at boot
    > iface lo inet loopback` - calls the network interface

  - **/etc/resolv.conf** - this file defines how the your linux instance uses DNS to resolve host names.  It basically lists the DNS names that the host system uses for resolution.  It normally contains the DNS generated by DHCP.

### How to Setup an Interface with DHCP by Editing the /etc/network/intefaces file

> auto InterfaceName  
> allow-hotplug InterfaceName  
> iface InterfaceName inet dhcp  

  Where allow-hotplug will start the interface upon event detection.

## NetworkManager

- NetworkManager is a utility that is is used to manage both network and network interface cards in Linux.
- It is an addition to the previously mentioned config files and can be disabled if necessary.  Both editing the config files and using NetworkManager do the same thing so the choice is yours as to which one you are more comfortable using.
- NetworkManager has several related utilities that it uses.  These are:

  - IP utility
  - nmcli - NetworkManager Command Line
  - nmtui - NetworkManager Text User Interface (text based configuration interface)

- One of the more notable changes with NetworkManager is instead of using `ifconfig` to get network information, we now invoke the IP utility and use `ip a`.
- ***On Rhel derived linux variants, the NetworkManager stores new network profiles in keyfile format in the /etc/NetworkManager/system-connections/ directory.***

## Navigating NetworkManager

- to check if NetworkManager is running on your system: `systemctl status NetworkManager`
- to locate the network config files for NetworkManager: `cd /etc/NetworkManager`
- to locate the connecting settings: `cd /etc/NetworkManager/system-connections`
- to see a list of all network devices on a system: `nmcli device`
- to see the properties of all network devices on a system: `nmcli device show`
- to see the properties of an individual device on a system: `nmcli device show *deviceName*`
- to see all existing connections: `nmcli connection`
- to see the properties of a connection: `nmcli connection show *deviceName*`
- to check network connectivity: `nmcli networking connectivity`
  This will output one of five(5) results:
  - **none**: the host is not connected to any network.
  - **portal**: the host is behind a captive portal and cannot reach the full Internet.
  - **limited**: the host is connected to a network, but it has no access to the Internet.
  - **full**: the host is connected to a network and has full access to the Internet.
  - **unknown**: the connectivity status cannot be found out.

## Configuring Network Settings With NetworkManager

### Configure Network Adapter with Dyamic IP

`sudo nmcli connection add type ethernet ifname *yourInterfaceName* con-name *giveconnectionaname*`

### Configure Network Adapter with Static IP

`nmcli connection add type ethernet ifname *yourInterfaceName* con-name *giveconnectionaname* ip4 192.168.100.69/24 gw4 192.168.100.1`

### Modifying a Connection

`sudo nmcli connection modify *connectionname* ipv4.DNS 8.8.8.8`

### Enabling a connection

`nmcli connection up connectionname`

### Disabling a connection

`nmcli connection down connectionname`

## Other Network Commands

- **netstat**:  stands for Network statistics. It displays information about different interface statistics, including open sockets, routing tables, and connection information. Further, it can be used to displays all the socket connections (including TCP, UDP). Apart from connected sockets, it also displays the sockets that are pending for connections. It is a handy tool for network and system administrators.  *use "man netstat" for more information*

- **tcpdump**: prints out a description of the contents of packets on a network interface.  It is used to monitor traffic on a particular interface going in both directions.

  - The syntax to run tcpdump is: `tcpdump -i interfaceName`

- **ethtool**: used to provide information about the network interface cards on your linux device.  In order to use this command you must first know the names of the interface cards in your device which can be found using - `ip a`.

  - The syntax for using ethtool is: `ethtool interfaceName` eg: `ethtool ens18`.

  - *Note*: the lo interface is a special interface that is a computer uses to communicate with itself and is mainly used for diagnostics and troubleshooting.

  - Check man pages for more options with ethtool.

- **NIC Bonding**: also known as network bonding, is defined as the aggregation or combination of multiple NICs into a single bond interface providing HA and redundancy.

- **wget**: used to download files and applications.  

  - The syntax to use this command is `wget http://full-url`

- **curl**:  curl  is  a  tool for transferring data from or to a server.  If not told otherwise, curl writes the received data to stdout. It can be  instructed to  instead save that data into a local file, using the -o, --output or -O, --remote- name options.

  - The syntax for the curl command is `curl option url`

  - curl can also be used to test if a website is up by using the address of the website.  If after running the curl command you are presented with html coding for the webpge it means the website is up and running.  In which case it will return: `curl: (6) Could not resolve .....`.

- **ping**: the ping command is used to test if a host is reachable.

  - The syntax for the ping command is `ping option host(url or IP)`

- **ftp**:  allows a user to transfer files to and from a remote network server.

  - both the source server and the destination server should be running the ftp daemon, vsftpd

  - Syntax for ftp:
  
  > `ftp remoteServerAddress`.  This will prompt for a username and password.
  > After the credentials have been added, to transfer a file type: `put filename`
  > To exit: `bye`

- **scp**: used copy files between hosts on a network.  It uses ssh(1) for data transfer, and uses the same authentication and provides the same security as a login
session. It will ask for passwords or passphrases if they are needed for authentication.

  - The syntax for using scp is: `scp fileToTransfer destinationServer:/copy_to_location/on/destinationServer`

- **rsync**: fast and extraordinarily versatile file copying tool.  It can copy locally, to/from another host over any remote shell, or to/from a remote rsync daemon.  
It offers a large number of options that control every aspect of its behavior and permit very flexible specification of the set of files to be copied.

  - The syntax for rsync when pulling a file via remote shell is: `rsync [OPTION...] [USER@]HOST:SRC... [DEST]`
  - The syntax for rysnc when pushing a file via remote shell is: `rsync [OPTION...] SRC... [USER@]HOST:DEST`

**nslookup**: used to obtain a domain name, IP address and DNS records.  The user enters the hostname of the server it wants to query and nslookup returns the IP and DNS record for the server.  It can be used in interactive and non-interactive mode.  

- The syntax for a nslookup command is: `nslookup`.  This will generate a prompt where you can enter the hostname of the device you wish to query.  Type exit when finished.  The output generated by the query is broken down below:

  > Server: the DNS servers used
  > Address: the IPV6 address
  > Non-Authoritative Answer -
  > Name - URL that shows where the data was pulled from
  > Addresses: IP Address of where the data was pulled from

**dig** - The dig command in Linux is used to gather DNS information. It stands for Domain Information Groper, and it collects data about Domain Name Servers. The dig command is helpful for troubleshooting DNS problems, but is also used to display DNS information.

- If dig is not installed on your system, it can be installed using: `sudo apt-get install dnsutils`.

- The syntax for using dig is: `dig [server] [name] [type]` where:
  - server - The hostname or IP address the query is directed to
  - name - The DNS (Domain Name Server) of the server to query
  - type - the type of DNS record to retrieve. By default (or if left blank), dig uses the A record type

- Example ***`dig google.com`***
  - The above command will generate several peices of information, the most important being the "answer section".
    - The first column lists the name of the server that was queried
    - The second column is the Time to Live, a set timeframe after which the record is refreshed
    - The third column shows the class of query – in this case, “IN” stands for Internet
    - The fourth column displays the type of query – in this case, “A” stands for an A (address) record
    - The final column displays the IP address associated with the domain name

  - By adding `any` to the end of the command, The system will list all google.com DNS records that it finds, along with the IP addresses.

**traceroute** - used to map the route a packet takes from source to destination.  It is often used to diagnose network issues.  Each hop represents a new server or router that the packet passes through. It can also help you to determine where there might be a slow connection along the path.

- The syntax for using traceroute is: `traceroute address/ipaddress`

## Package Management in Ubuntu and Other Debian Derived Distros

- Ubuntu’s package management system is derived from the same system used by the Debian GNU/Linux distribution. The package files contain all of the necessary files, meta-data, and instructions to implement a particular functionality or software application on your Ubuntu computer.

- Debian package files typically have the extension `.deb`, and usually exist in repositories which are collections of packages found online.  Many packages use dependencies. Dependencies are additional packages required by the principal package in order to function properly.

- The apt command is a powerful command-line tool, which works with Ubuntu’s Advanced Packaging Tool (APT) performing such functions as installation of new software packages, upgrade of existing software packages, updating of the package list index, and even upgrading the entire Ubuntu system.

  - To install a package: `sudo apt install packageName`
  - To remove a package: `sudo apt remove packageName` (**To remove multiple packages, seperate them by spaces**)
  - To remove a package and its config files: `sudo apt remove --purge packageName`.
  - To update the package index: `sudo apt update`. The APT package index is essentially a database of available packages from the repositories defined in the `/etc/apt/sources.list` file and in the `/etc/apt/sources.list.d` directory.
  - To upgrade packages: `sudo apt upgrade`
  - ***Note***: Actions of the apt command, such as installation and removal of packages, are logged in the `/var/log/dpkg.log` log file.

### dpkg

- dpkg is a package manager for Debian-based systems. It can install, remove, and build packages, but unlike other package management systems, it cannot automatically download and install packages or their dependencies. ***Apt and Aptitude are newer, and layer additional features on top of dpkg.***

  - To list all packages in the system’s package database: `dpg -l`
  - To list the files installed by a particular package: `dpkg -L packageName`
  - To find out which package installed a file: `dpkg -S /path/filename.extension`
  - To install a local *.deb* file: `sudo dpkg -i file.deb`
  
## Services

### DNS

- DNS = Domain Name System. The purpose of DNS is to translate IP addresses to human readable domain names.
- In ubuntu and other debian derived distros the DNS config file is `/etc/bind/named.conf`.

### NTP

- Network Time Protocol is used for time synchronization.
- To install the service: `sudo apt install ntp`
- Location of config file: `/etc/ntp.conf`
- To start the service: `sytstemctl start ntpd`
- Allow connections through firewall: `sudo ufw allow from any to any port 123 proto udp`
- To query the ntp servers running on a server: `ntpq`.  ntpq ,operates in interactive mode and takes arguments such as -p to show all peers.
- To stop the service: `systemctl stop ntpd`

