# Initial Server Setup

These are the steps that should be taken after a linux server installation:

- Update your system: `sudo apt update && sudo apt upgrade -y`
- Clean up updates: `sudo apt autoremove && sudo apt clean`
- If not installed during setup, install ssh: sudo apt `install openSSH`

## Add users

- To add a user run: `sudo adduser username`
- Add the user to the sudo group: `sudo usermod -aG sudo username`
- Add/update user password: `sudo passwd username`

## Secure & Harden the System

- Change the root user password: `sudo passwd root`
- Disble remote access login:
  - To generate SSH key, on the computer you intend to use to remotely connect to your server run the following command: `ssh-keygen`.  The default location of the generated file on Windows is: 'C:\Users\<user>\.ssh\id_rsa'.
  - Next, on the same machine that will be used to connect to the remote server, navigate to the directory where the generated key is and run the following command to copy that key to the remote server: `ssh-copy-id user@remote_server_ip`
- Disable Password Login **(Optional)**:
  - Use a text editor and open '/etc/ssh/sshd_config' file
  - Locate the *PasswordAuthentication yes* line, remove the hashtag(#) and change 'yes' to 'no'.
  - Save and close the file.
- Disable Root Login:
  - Use a text editor and open '/etc/ssh/sshd_config' file
  - Locate the *PermitRootLogin prohibit-password* line, replace 'prohibit-password' to 'no'.
  - Save and close the file.

- After making any change that affects SSH and login, it is good practice to restart the SSH service: `sudo systemctl restart SSH`

- Firewall:
  - To see which apps are registered with the ufw firewall: `sudo ufw app list`
  - To make the firewall allow connections for an application: `sudo ufw allow appName`
  - To check firewall status: `sudo ufw status`
  - To enable firewall: `sudo ufw enable`
