# Installation 

## Walkthrough 

```
sudo apt install postgresql
sudo add-apt-repository ppa:mrazavi/gvm
sudo apt install gvm

sudo -u gvm -g gvm greenbone-nvt-sync
sudo -u gvm -g gvm greenbone-feed-sync --type CERT
sudo -u gvm -g gvm greenbone-feed-sync --type SCAP
sudo -u gvm -g gvm greenbone-feed-sync --type GVMD_DATA

# To remove NVT db, and rebuild it from the scanner:

export $(sudo cat /etc/default/gvmd-pg)
sudo -E -u gvm -g gvm gvmd --rebuild

# You can access the Greenbone Security Assistant web interface at:

http://localhost:9392

The default username/password is as follows:

Username: admin
Password: admin

You can check the status of greenbone daemons with systemctl:

systemctl status ospd-openvas # scanner
systemctl status gvmd # manager
systemctl status gsad # web ui


```


## Documentation 

  * https://launchpad.net/~mrazavi/+archive/ubuntu/gvm
