# Troubleshooting SELinux Centos 


```
# Find out which problems you had 
cd /var/log/audit 
sealert -a audit.log > report.log

# Alternative - look into messages and find uid 
vi messages
sealert -l de929621-a863-4f2f-ac74-4453138c8c08

# With both you answers how to proceed 
# in case of a port missing 
# e.g. 
# which port type belongs to 80 
semanage port -l | grep 80 
# add you port to that list 
semanage port -a -t http_port_t -p tcp 85

```
