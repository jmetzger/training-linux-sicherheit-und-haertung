# OpenVas 

## Vagrant 

```
virtualbox 
vagrant 
git for windows 
# 
mkdir ubuntu 
cd ubuntu
vagrant init  
```

## Installation for version GVM 20.08 (2021-05-19) 

```
Variant 1:
Install on Ubuntu Server 20.04:
as follows:
https://launchpad.net/~mrazavi/+archive/ubuntu/gvm

or 
Variant 2:
docker-container 
https://github.com/admirito/gvm-containers
```


## Installation for version GVM 11 


#  OpenVAS (Ubuntu 20.04LTS)

## Requirements 

  * tested with 1 GB and 25 GB -> does not work, 
    df -> 100% // GMP error during authentication -> when trying to login 
  * tested with 2 GB and 50 GB -> WORKS !

## openvas -> gvm (Greenbone Vulnerability Management) / mrazavi 

```
Installation on Ubuntu 20.04 LTS
https://launchpad.net/~mrazavi/+archive/ubuntu/gvm
# https://www.osboxes.org/ubuntu/
# Done with vagrant init ubuntu/focal64 instead 

# postgresql is needed
sudo apt install -y postgresql 
sudo add-apt-repository ppa:mrazavi/gvm
sudo apt install -y gvm
# only from one machine (when same source ip) at a time 
greenbone-nvt-sync
sudo greenbone-scapdata-sync
sudo greenbone-certdata-sync

You can access the Greenbone Security Assistant web interface at:

https://localhost:9392

The default username/password is as follows:

Username: admin
Password: admin

You can check the status of greenbone daemons with systemctl:

systemctl status ospd-openvas # scanner
systemctl status gvmd # manager
systemctl status gsad # web ui

# change /etc/default 
https://<ip>:9392

```

Documentation 
https://docs.greenbone.net/GSM-Manual/gos-20.08/en/web-interface.html

## PDF - Generation 

```
# 2 packages are needed for the pdf-generation:
apt install -y texlive-latex-extra --no-install-recommends
apt install -y texlive-fonts-recommended
# after having installed these, pdf generation works ! 

```

