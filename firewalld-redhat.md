# firewalld (centos 9 / rocky 9)  

## Is firewalld running ?
```
# is it set to enabled ?
systemctl status firewalld 
firewall-cmd --state
```

## Command to control firewalld 
  
  * firewall-cmd 

## Best way to add a new rule 
```
# Step1: do it persistent -> written to disk 
firewall-cmd --add-port=82/tcp --persistant 

# Step 2: + reload firewall 
firewall-cmd --reload 
```

## Zones documentation 

man firewalld.zones 

## Zones available 

```
firewall-cmd --get-zones 
block dmz drop external home internal public trusted work
```

## Active Zones 

```
firewall-cmd --get-active-zones
# in our case empty 
```

## Show information about all zones that are used 
```
firewall-cmd --list-all 
firewall-cmd --list-all-zones 
```


## Add Interface to Zone ~ Active Zone 

```
firewall-cmd --zone=public --add-interface=enp0s3 --permanent 
firewall-cmd --reload 
firewall-cmd --get-active-zones 
public
  interfaces: enp0s3

```
## Default Zone 

```
# if not specifically mentioned when using firewall-cmd
# .. add things to this zone 
firewall-cmd --get-default-zone
public

```

## Show services / Infos services 
```
firewall-cmd --get-services
# Infos, what can it do 
firewall-cmd --info-service=ssh

```

## Adding/Removing a service 

```
# lange Form für Laufzeit 
firewall-cmd --zone=public --add-service=http
# kurze Form / nimmt default target -> zone: public 
firewall-cmd --add-service=http

firewall-cmd --list-all
firewall-cmd --list-all --permanent

firewall-cmd --runtime-to-permanent
# Here it should show up 
cat /etc/firewalld/zones/public.xml 
```

## Walkthrough apache / adding Port (Centos 8 / Redhat 8 with enabled SELinux (by default))

```

# /etc/httpd/conf/httpd.conf 
# add port Listen 82 
# Try to restart - not working port cannot be bound 
sealert -a /var/log/audit/audit.log 
# we will get this info to allow this port 
semanage port -a -t http_port_t -p tcp 82
# start apache 
systemctl start httpd
firewall-cmd --add-port=82/tcp --zone=public --permanent

```

## Enable / Disabled icm 
```
firewall-cmd --get-icmptypes
# none present yet 
firewall-cmd --zone=public --add-icmp-block-inversion --permanent
firewall-cmd --reload
```

## Working with rich rules 
```
# Documentation 
# man firewalld.richlanguage

# throttle connectons 
firewall-cmd --permanent --zone=public --add-rich-rule='rule family=ipv4 source address=10.0.50.10/32 service name=http log level=notice prefix="firewalld rich rule INFO:   " limit value="100/h" accept' 
firewall-cmd --reload # 
firewall-cmd --zone=public --list-all

# port forwarding 
firewall-cmd --get-active-zones
firewall-cmd --zone=public --list-all
firewall-cmd --permanent --zone=public --add-rich-rule='rule family=ipv4 source address=10.0.50.10 forward-port port=42343 protocol=tcp to-port=22'
firewall-cmd --reload 
firewall-cmd --zone=public --list-all
firewall-cmd --remove-service=ssh --zone=public

# 


# list only the rich rules 
firewall-cmd --zone=public --list-rich-rules

# persist all runtime rules 
firewall-cmd --runtime-to-permanent




```


## References 

  * https://www.linuxjournal.com/content/understanding-firewalld-multi-zone-configurations#:~:text=Going%20line%20by%20line%20through,or%20source%20associated%20with%20it.
  * https://www.answertopia.com/ubuntu/basic-ubuntu-firewall-configuration-with-firewalld/
