# Remote rsyslog - loging (Centos 8) 

## Change on server 1 (main) 

```
cd /etc/
# changed
#vi rsyslog.conf 
# uncommented these 4 lines 
# Provides UDP syslog reception
# for parameters see http://www.rsyslog.com/doc/imudp.html
module(load="imudp") # needs to be done just once
input(type="imudp" port="514")

# Provides TCP syslog reception
# for parameters see http://www.rsyslog.com/doc/imtcp.html
module(load="imtcp") # needs to be done just once
input(type="imtcp" port="514")

# restart rsyslog - daemon
systemctl restart rsyslog.service 
```

## Change on server 2 (secondary) 

```
# added hostname in /etc/hosts 
# in the case main has 192.168.33.10 
echo "192.168.33.10 main" >> /etc/hosts 

# Added to line at then end of /etc/rsyslog.conf 
# log to udp (@) AND tcp (@@)
# In production you only need one of those 
*.*    @main
*.*    @@main

# Restart service 
systemctl restart rsyslog.service 

```

## Finally testing 

```
# on secondary 
logger -p local0.info "Testmessage from this beautiful team" 

# on main
# we should have an output 
cat /var/log/messages | grep -i testmessage 
```
