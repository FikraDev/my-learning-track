# Install and Setup rsyslog on Ubuntu

- rsylog is a utility that is used to forward log messages in a client-server model.
- When configured as a client, it sends logs to a remote server over the network via TCP/UDP protocols.
- As a server, it receives logs over the network from remote client on port 514 TCP/UDP or any custom port on which it is configured to listen on.
- Rsyslog is the default syslogd on Debian systems and is usually installed on Ubuntu by default.

- To check is ryslog is installed: `apt list -a rsyslog` or `syslog --version`

## Install rsyslog

- To install rsyslog: `sudo apt update` then `sudo apt install rsyslog -y`
- Once the application is installed enable it: `sudo systemctl enable --now rsyslog`

## Setup a device as rsyslog server

- open the ryslog config file: `sudo vim /etc/rsyslog.conf`
- rsyslog to use both UDP and TCP protocols for logs reception over the ports **514 and 50514** respectively.  By default syslog uses UDP port 514.  There to enable UDP syslog reception:
  - in the modules section, uncomment the lines under *'# provides UDP syslog reception'*.
  - optionally you can enable reception under TCP instead by following the steps outlined previously.
- Save and exit the file
- Restart the service `sudo systemctl restart rsyslog`.
- Verify that the service is running: `sudo ss -4altunp | grep 514`
- If firewall is running, allow rsyslog through: `sudo ufw allow 514/udp` and `sudo ufw allow 50514/tcp`

