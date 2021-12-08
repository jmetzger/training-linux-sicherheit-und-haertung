# Using SE Linux booleans 

## Find out, which are available 

```
getsebool -a | grep nis 
# shows all booleans with short description 
semanage boolean -l 
```

## Prepare using sesearch

```
dnf whatprovides search
dnf install -y setools-console
```

## Find out, which rules are triggered by boolean 

```
# -A shows allow rules 
sesearch -b nis_enabled -A

# If there are a lot, considers using, e.g. semanage for opening specific ports 
# like mentioned after using 
# sealert -a /var/log/audit/audit.log 

```

## Are there booleans for my specific use case 

```
sesearch -s init_t -t unreserved_port_t -A
#
```

## Activating a boolean (selinux) 

```
# only till next report 
setsebool nis_enabled 1 

# persistent 
setsebool -P nis_enabled 1 

# is it activated 
getsebool nis_enabled 
```

## Reference 

  * https://wiki.gentoo.org/wiki/SELinux/Tutorials/Using_SELinux_booleans

```
# -C option in sesearch seems deprecated in Centos 
```
