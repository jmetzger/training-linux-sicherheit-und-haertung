# SELinux 

## Commands 

```
sestatus 
# Regeln nicht durchsetzen bis zum nächsten Boot
# wenn das System auf Enforcing steht
setenforce 0

# Status abfragen
getenforce 
sestatus 

# config - selinux aktivieren / deaktivieren
/etc/selinux/config 


```

## Force relabeling of files  

```
touch /.autorelabel 
# important - might take some time 
reboot
```
