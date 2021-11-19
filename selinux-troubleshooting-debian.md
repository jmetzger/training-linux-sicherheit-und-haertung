# Troubleshooting SELinux Debian 

```
# Situation: Permission denied with ssh after setting enforcing mode 

# How to deal ? 
cd /var/log/audit 

# get some hints, e.g. use audit2why
cat audit.log | audit2why 

# Created a module we can install, if we want 
cat audit.log | grep 'comm="sshd"' | audit2allow -M sshaccess 

# Look what the module does in same 
cat sshallow.te

# Got an hint we can active bool -> ssh_sysadm_login 
setsebool -P ssh_sysadm_login 0

# finally check if you can login by ssh

```
