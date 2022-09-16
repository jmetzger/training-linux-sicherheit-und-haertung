# Installation 

## Walkthrough 

```
sudo apt install postgresql
sudo add-apt-repository ppa:mrazavi/gvm
sudo apt install gvm

# Does not work 
#sudo -u gvm -g gvm greenbone-nvt-sync
#sudo -u gvm -g gvm greenbone-feed-sync --type CERT
#sudo -u gvm -g gvm greenbone-feed-sync --type SCAP
#sudo -u gvm -g gvm greenbone-feed-sync --type GVMD_DATA
sudo runuser -u _gvm -- greenbone-nvt-sync
sudo runuser -u _gvm -- greenbone-feed-sync --type CERT
sudo runuser -u _gvm -- greenbone-feed-sync --type SCAP
sudo runuser -u _gvm -- greenbone-feed-sync --type GVMD_DATA



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

## Fixing pdf-export problems 

```
apt install -y texlive-latex-extra --no-install-recommends
apt install -y texlive-fonts-recommended
# after having installed these, pdf generation works ! 
```

## Alternative Installation 

  * https://github.com/admirito/gvm-containers


## Documentation 

  * https://launchpad.net/~mrazavi/+archive/ubuntu/gvm
