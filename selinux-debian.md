# SELinux Debian 

## Walkthrough 

```
apt-get install selinux-basics selinux-policy-default auditd
selinux-activate
reboot

# for checking
# Also refer to our other documents 
# e.g. apache walkthrough
setenforce 1 

check-selinux-installation 
echo $?
```

## Howto on Debian 

  * https://wiki.debian.org/SELinux/Setup
