# Block / Allow specific mac (Exercise on Rocky)

## Drop specific mac 

```
# Default Zone: public 
# machine 2 : 192.168.56.103
# MAC from machine1 
firewall-cmd --add-rich-rule='rule source mac=08:00:27:ae:1a:7d drop'
```

```
# Test from machine 192.168.56.102
ping 192.168.56.103
```  

## Only allow specific mac / disallow other 

```
# windows get mac of machine
cmd.exe
```

```
# windows -> get mac from 192.168.56.1 - interface 
ipconfig /all 
```



```
# machine 2: 192.168.56.103
# Lauschen auf icmp 
tcpdump -i enp0s8 icmp 

# windows
ping 192.168.56.103 

# machine 2: 192.168.56.103 
# allow only from this mac -> Windows machine
# rewrite - to ":" 
firewall-cmd --zone=drop --add-rich-rule='rule source mac=08:00:27:ae:1a:7d allow'
firewall-cmd --zone=drop --change-interface=enp0s8

firewall-cmd --list-all-zones
```

```
# now try to ping from windows
# cmd.exe
# works 
ping 192.168.56.103 

```

```
# now try to ping from ubuntu 
ping 192.168.56.103 

```

## Reset after exercise
firewall-cmd --zone=public --change-interface=enp0s8
```
