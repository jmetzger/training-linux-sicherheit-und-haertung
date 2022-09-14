# Tripwire 

```
HIDS: Tripwire
Lab: Tripwire Install
# Debian
apt install tripwire
# Answer the questions as follows:
# Site
# Schlüssel erzeugen -> Ja
# Lokalen Schlüssel erzeugen -> Ja
# Tripwire - Konfigurationsdatei erzeugen -> Ja
# Policies -> Ja
Tripwire - What is where ?
Binaries: /usr/sbin
Database: /var/lib/tripwire
Tripewire - Keys
site key : Secure configuration files (may not be modified)
local key: Protect binary files
Tripwire - configuration file
If you have not created that during installation
# Creates encrypted twpol - file
sudo twadmin --create-polfile /etc/tripwire/twpol.txt
# create database
sudo tripwire --init
Last update: 2019/07/31
08:23 trainingmaterial-linux-security-3days http://localhost/dokuwiki/doku.php?id=trainingmaterial-linux-security-3days
http://localhost/dokuwiki/ Printed on 2019/07/31 08:25
Tripwire - check (document)
We want to document what gets scanned
tripwire --check | grep Filename > test_results'
#If we view this file, we should see entries that look like this:
less /etc/tripwire/test_results
# ...
Filename: /etc/rc.boot
Filename: /root/mail
Filename: /root/Mail
Filename: /root/.xsession-errors
Tripwire - adjust twpol.txt
# replace /proc by /proc/devices
# was:
#/proc -> $(Device) ;
# now
/proc/devices -> $(Device) ;
# remove all /root/* entries that are not present
# e.g.
# /root/.sawfish
# uncomment /var/lock and /var/run
#/var/lock -> $(SEC_CONFIG) ;
#/var/run -> $(SEC_CONFIG) ; # daemon PIDs
Tripwire - recreate pol file + re-init db
# polfile
sudo twadmin -m P /etc/tripwire/twpol.txt
# re-init database
sudo tripwire --init
Tripwire - rerun check
sudo tripwire --check
Tripwire - remove sensitive information
sudo rm /etc/tripwire/test_results
sudo rm /etc/tripwire/twpol.txt
# recreate it
sudo twadmin --print-polfile > /etc/tripwire/twpol.txt
2019/07/31 08:25 13/56
Training materials / Schulungsunterlagen - http://localhost/dokuwiki/
sudo rm /etc/tripwire/twpol.txt

```
