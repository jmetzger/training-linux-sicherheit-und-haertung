# OpenVas 

## Installation for version GVM 11 

```
# Refering to: https://launchpad.net/~mrazavi/+archive/ubuntu/gvm
sudo add-apt-repository ppa:mrazavi/gvm
# installation commands is different for 11 
sudo apt install gvm

greenbone-nvt-sync
sudo greenbone-scapdata-sync
sudo greenbone-certdata-sync

systemctl status ospd-openvas # scanner
systemctl status gvmd # manager
systemctl status gsad # web ui

```

## openvas -> gvm (Greenbone Vulnerability Management) / mrazavi 

```
Installation on Ubuntu 20.04 LTS
https://launchpad.net/~mrazavi/+archive/ubuntu/gvm
https://www.osboxes.org/ubuntu/

https://<ip>:9392

(The port number has changed according to the upstream in the new version and the old 4000 port number is no longer the default)

The default username/password is as follows:

Username: admin
Password: admin

You can check the status of greenbone daemons with systemctl:

systemctl status ospd-openvas # scanner
systemctl status gvmd # manager
systemctl status gsad # web ui

```
