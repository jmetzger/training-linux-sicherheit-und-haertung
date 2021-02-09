# OpenVas 

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
